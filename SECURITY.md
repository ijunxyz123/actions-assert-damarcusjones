ijunxyz123:main.githubjobs:
  build-image:
    runs-on: ubuntu-latest
    env:
      archive: "oci-image.tar"
    steps:
      - uses: docker/setup-buildx-action@v1
      - uses: docker/setup-qemu-action@v1
      - name: Build Docker Image
        uses: docker/build-push-action@v2
        with:
          labels: "${{ steps.meta.outputs.labels }}"
          outputs: "type=oci,dest=${{ env.archive }}"
          tags: "${{ steps.meta.outputs.tags }}"
          platforms: linux/amd64,linux/arm64,linux/arm/v7
      - name: Log in to GitHub Container Registry as actor
        uses: docker/login-action@v1
        with:
          registry: ghcr.io
          username: "${{ github.repository_owner }}"
          password: "${{ secrets.GHCR_PAT }}"
      - name: Push OCI archive to remote registry
        uses: pr-mpt/actions-push-oci-archive-to-registry
        with:
          archive: ${{ env.archive }}steps.meta.outputs.labelssteps.meta.outputs.tagsenv.archivepr-mpt/actions-push-oci-archive-to-registry@v1ghcr.iohttps://github.com/ijunxyz123/actions-push-oci-archive-to-registry-damarcusjones.git# Security Policy

## Supported Versions

Use this section to tell people about which versions of your project are
currently being supported with security updates.

| Version | Supported          |
| ------- | ------------------ |
| 5.1.x   | :white_check_mark: |
| 5.0.x   | :x:                |
| 4.0.x   | :white_check_mark: |
| < 4.0   | :x:                |

## Reporting a Vulnerability

Use this section to tell people how to report a vulnerability.

Tell them where to go, how often they can expect to get an update on a
reported vulnerability, what to expect if the vulnerability is accepted or
declined, etc.
