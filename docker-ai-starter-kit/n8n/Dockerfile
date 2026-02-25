FROM n8nio/n8n

USER root

# Install Python, pip AND libraries for compilation (needed for lxml/docx)
RUN apk add --update --no-cache \
    python3 \
    py3-pip \
    build-base \
    libxml2-dev \
    libxslt-dev \
    python3-dev

# Install python-docx globally (as root)
RUN pip3 install python-docx --break-system-packages openpyxl

# (Optional) Post-build garbage removal to reduce size (can be skipped)
# RUN apk del build-base python3-dev

# Switch back to the n8n user for security
USER node