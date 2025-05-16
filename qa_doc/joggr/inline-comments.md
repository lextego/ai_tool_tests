<!--@@joggrdoc@@-->
<!-- @joggr:version(v2):end -->
<!-- @joggr:warning:start -->
<!-- 
  _   _   _    __        __     _      ____    _   _   ___   _   _    ____     _   _   _ 
 | | | | | |   \ \      / /    / \    |  _ \  | \ | | |_ _| | \ | |  / ___|   | | | | | |
 | | | | | |    \ \ /\ / /    / _ \   | |_) | |  \| |  | |  |  \| | | |  _    | | | | | |
 |_| |_| |_|     \ V  V /    / ___ \  |  _ <  | |\  |  | |  | |\  | | |_| |   |_| |_| |_|
 (_) (_) (_)      \_/\_/    /_/   \_\ |_| \_\ |_| \_| |___| |_| \_|  \____|   (_) (_) (_)
                                                              
This document is managed by Joggr. Editing this document could break Joggr's core features, i.e. our 
ability to auto-maintain this document. Please use the Joggr editor to edit this document 
(link at bottom of the page).

Documentation research and outputs by LexTego Ltd.
Licensed under the Creative Commons Attribution-ShareAlike 4.0 International License.
See: https://creativecommons.org/licenses/by-sa/4.0/
-->
<!-- @joggr:warning:end -->
```yaml
# SPDX-License-Identifier: Apache-2.0
version: "2"  # Specify the version of the Docker Compose file format

services:
  node:  # Define a service named 'node' (the main application)
    container_name: tms-service  # Set the container name to 'tms-service'
    build:
      context: .  # Build the Docker image from the current directory
      args:
        - GH_TOKEN  # Pass the GH_TOKEN build argument (for private repo access, if needed)
    restart: "no"  # Do not automatically restart the container if it stops
```

**Notes:**

* This Compose file defines a single service (`node`) for the application.

* The `build` section allows you to pass build arguments (like `GH_TOKEN`) and sets the build context.

* `restart: "no"` means the container will not be restarted automatically if it exits.

* You can extend this file to add more services (e.g., databases, cache) as needed for your stack.

<!-- @joggr:editLink(fa8b2a6d-103e-4d10-ad6e-640d2de9b77b):start -->
---
<a href="https://app.joggr.io/app/documents/fa8b2a6d-103e-4d10-ad6e-640d2de9b77b/edit">
  <img src="https://cdn.joggr.io/assets/static/badges/joggr-document-edit.svg?did=fa8b2a6d-103e-4d10-ad6e-640d2de9b77b" alt="Edit doc on Joggr" />
</a>
<!-- @joggr:editLink(fa8b2a6d-103e-4d10-ad6e-640d2de9b77b):end -->
