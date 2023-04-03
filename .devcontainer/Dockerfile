FROM docker.io/zmkfirmware/zmk-dev-arm:3.0

ARG ZMK_URL
ARG ZMK_BRANCH
ARG ZMK_PATH

# clone zmk
RUN git clone --filter=tree:0 --single-branch --branch=${ZMK_BRANCH} ${ZMK_URL} ${ZMK_PATH}

# buil zmk
RUN cd ${ZMK_PATH} && \
    west init -l app/ && \
    west update && \
    cd /

# copy .bashrc with build functions
COPY .bashrc tmp
RUN mv /tmp/.bashrc ~/.bashrc