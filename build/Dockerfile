FROM python:3.11.3-bullseye
ARG JUPYTER_USER=jupyter
ARG JUPYTER_UID=1000
ARG JUPYTER_GROUP=jupyter
ARG JUPYTER_GID=1000
ENV USER ${JUPYTER_USER}
ENV HOME /home/${JUPYTER_USER}
RUN groupadd -g ${JUPYTER_GID} ${JUPYTER_GROUP} && \
    useradd -m -s /bin/bash -N -u ${JUPYTER_UID} -g ${JUPYTER_GID} ${JUPYTER_USER} && \
    mkdir -p /home/${JUPYTER_USER} && \
    chown ${JUPYTER_USER}:${JUPYTER_GROUP} /home/${JUPYTER_USER}
ENV SHELL="/bin/bash"
ENV TZ=Asia/Tokyo
ENV PYTHONIOENCODING utf-8
ARG DEBIAN_FRONTEND=noninteractive
ARG TARGETARCH
RUN apt-get update && apt-get install -y wget curl unzip gnupg2 tzdata python3-pip vim \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
RUN python3 -m pip install --no-cache-dir jupyterlab \
    black \
    jupyterlab_code_formatter \
    jupyterlab-git \
    lckr-jupyterlab-variableinspector \
    jupyterlab_widgets \
    ipywidgets \
    import-ipynb
WORKDIR ${HOME}
USER ${JUPYTER_USER}
CMD ["jupyter", "lab", "--ip=0.0.0.0", "--allow-root", "--no-browser", "--NotebookApp.token=''"]
