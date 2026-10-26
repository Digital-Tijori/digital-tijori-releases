# Digital Tijori: downloads

Installers for [Digital Tijori](https://digital-tijori.prajwalrajup.in) (macOS, Windows, Linux). The app's source is private; this repo holds only the built installers and the workflow that builds them.

Get the latest from the [Releases](../../releases/latest) page, or from the download button on the website. You need a license to use the app: it asks for the email you paid with.

## How a release is made (maintainers)
1. Publish a release in the app repo (tag `vX.Y.Z`). The build writes that version into the app source before building, so there is no version to edit first.
2. The app repo's workflow starts **Build installers** here. It builds macOS (Apple silicon and Intel), Windows and Linux and attaches them to a release with the same tag.
3. Secrets and variables of this repo: secret `APP_REPO_TOKEN` (fine-grained token, **Contents: read** on the app repo only); variables `TIJORI_LICENSE_URL` and `TIJORI_LICENSE_PUBKEYS`.

The workflow only runs when started by the app repo or by hand; it never runs for pull requests.
