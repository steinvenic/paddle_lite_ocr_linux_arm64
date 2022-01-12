# paddle_lite_ocr_linux_arm64
#

FROM ubuntu:16.04

RUN apt-get update && apt-get install -y --no-install-recommends gcc g++ make wget unzip libopencv-dev pkg-config libssl-dev libgtk-3-dev
COPY . /app

WORKDIR /app

RUN cp -r ./cxx/lib/libpaddle_light_api_shared.so /usr/lib \ 
&& wget --no-check-certificate https://cmake.org/files/v3.16/cmake-3.16.8.tar.gz \
&& tar -zxvf cmake-3.16.8.tar.gz;rm -fr cmake-3.16.8.tar.gz;cd cmake-3.16.8 \
&& ./configure \
&& make && make install \
&& apt clean \

WORKDIR /app
RUN ./build.sh

ENTRYPOINT ["/app/install/paddle_lite_ocr/paddle_lite_ocr"]
