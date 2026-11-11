# TEST (2026-11-11): Codespace builds failed with "Could not resolve archive.ubuntu.com" inside the docker-in-docker feature step.
# Hypothesis: the build container gets IPv6-only DNS answers but has no IPv6 route. Force IPv4 for apt, curl, wget and getaddrinfo BEFORE the
# features run (features are layered on top of the image built here, so these files are in place when they call apt/curl).
FROM mcr.microsoft.com/devcontainers/base:ubuntu-24.04
RUN printf 'Acquire::ForceIPv4 "true";\nAcquire::Retries "5";\n' > /etc/apt/apt.conf.d/99force-ipv4 \
 && printf 'precedence ::ffff:0:0/96 100\n' >> /etc/gai.conf \
 && printf 'ipv4\nretry = 5\nretry-connrefused\n' > /root/.curlrc \
 && printf 'inet4_only = on\ntries = 5\n' >> /etc/wgetrc
