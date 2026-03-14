Security: Host Validation in Homepage
Challenge
When accessing the Homepage dashboard via an IP address, the container initially returned a "Host Validation Failed" error.

Root Cause
Modern web applications often implement Host Header validation to prevent DNS Rebinding attacks. The dashboard was rejecting requests because the Host IP was not explicitly "trusted" in the application environment.

Remediation
I implemented the HOMEPAGE_ALLOWED_HOSTS environment variable within the Docker configuration to white-list the local server IP and localhost, ensuring secure access without compromising the underlying host security.
