# Build on CPU Linux/WSL/CI; no source code, datasets, or credentials in image.
FROM python:3.12.14-slim-bookworm
RUN apt-get update && apt-get install -y --no-install-recommends openssh-server ca-certificates libgl1 libglib2.0-0 procps coreutils && rm -rf /var/lib/apt/lists/* && rm -f /etc/ssh/ssh_host_*
COPY requirements/torch-versions.txt requirements/test-common.txt /opt/requirements/
RUN pip install --no-cache-dir -r /opt/requirements/torch-versions.txt --index-url https://download.pytorch.org/whl/cu128 && pip install --no-cache-dir -r /opt/requirements/test-common.txt
COPY environments/gpu/profile.json /opt/neuron/environment-profile.json
RUN mkdir -p /run/sshd /root/.ssh /workspace && chmod 700 /root/.ssh
EXPOSE 22
WORKDIR /workspace
CMD ["sh", "-c", "ssh-keygen -A && exec /usr/sbin/sshd -D"]
