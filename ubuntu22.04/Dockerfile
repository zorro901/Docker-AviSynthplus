FROM        ubuntu:22.04 AS base

WORKDIR     /tmp/workdir

RUN     apt-get -yqq update && \
        apt-get install -yq --no-install-recommends ca-certificates expat libgomp1 && \
        apt-get autoremove -y && \
        apt-get clean -y

FROM base as build

ENV         DEBIAN_FRONTEND=noninteractive

ENV         FFMPEG_VERSION=n5.0.1 \
            LSMASHSOURCE_VERSION=20200728 \
            AVISYNTHPLUS_VERSION=v3.7.2 \
            NASM_VERSION=2.15 \
            YASM_VERSION=1.3.0 \
            AOM_VERSION=v3.3.0 \
            FDKAAC_VERSION=2.0.2 \
            FONTCONFIG_VERSION=2.14.0 \
            FREETYPE_VERSION=2.12.1 \
            FRIBIDI_VERSION=1.0.12 \
            KVAZAAR_VERSION=2.1.0 \
            LAME_VERSION=3.100 \
            LIBASS_VERSION=0.16.0 \
            LIBPTHREAD_STUBS_VERSION=0.4 \
            LIBVIDSTAB_VERSION=1.1.0 \
            LIBXCB_VERSION=1.15 \
            XCBPROTO_VERSION=1.15 \
            OGG_VERSION=1.3.5 \
            OPENCOREAMR_VERSION=0.1.5 \
            OPUS_VERSION=1.3.1 \
            OPENJPEG_VERSION=2.5.0 \
            THEORA_VERSION=1.1.1 \
            VORBIS_VERSION=1.3.7 \
            VPX_VERSION=1.11.0 \
            WEBP_VERSION=1.2.2 \
            X264_VERSION=20191217-2245-stable \
            X265_VERSION=3.2.1 \
            XAU_VERSION=1.0.9 \
            XORG_MACROS_VERSION=1.19.3 \
            XPROTO_VERSION=7.0.31 \
            XVID_VERSION=1.3.7 \
            LIBXML2_VERSION=2.9.14 \
            LIBBLURAY_VERSION=1.3.1 \
            LIBZMQ_VERSION=4.3.4 \
            LIBSRT_VERSION=1.4.4 \
            LIBARIBB24_VERSION=1.0.3 \
            LIBPNG_VERSION=1.6.37 \
            HARFBUZZ_VERSION=4.3.0 \
            SRC=/usr/local

ARG         FREETYPE_SHA256SUM="efe71fd4b8246f1b0b1b9bfca13cfff1c9ad85930340c27df469733bbb620938 freetype-2.12.1.tar.gz"
ARG         FRIBIDI_SHA256SUM="2e9e859876571f03567ac91e5ed3b5308791f31cda083408c2b60fa1fe00a39d v1.0.12.tar.gz"
ARG         LIBASS_SHA256SUM="246091cf034b097dbe362c72170e6996f8d2c19ffe664ce6768ec44eb9ca5c1c 0.16.0.tar.gz"
ARG         LIBVIDSTAB_SHA256SUM="14d2a053e56edad4f397be0cb3ef8eb1ec3150404ce99a426c4eb641861dc0bb v1.1.0.tar.gz"
ARG         OGG_SHA256SUM="0eb4b4b9420a0f51db142ba3f9c64b333f826532dc0f48c6410ae51f4799b664 libogg-1.3.5.tar.gz"
ARG         OPUS_SHA256SUM="65b58e1e25b2a114157014736a3d9dfeaad8d41be1c8179866f144a2fb44ff9d opus-1.3.1.tar.gz"
ARG         THEORA_SHA256SUM="40952956c47811928d1e7922cda3bc1f427eb75680c3c37249c91e949054916b libtheora-1.1.1.tar.gz" 
ARG         VORBIS_SHA256SUM="0e982409a9c3fc82ee06e08205b1355e5c6aa4c36bca58146ef399621b0ce5ab libvorbis-1.3.7.tar.gz"
ARG         XVID_SHA256SUM="abbdcbd39555691dd1c9b4d08f0a031376a3b211652c0d8b3b8aa9be1303ce2d xvidcore-1.3.7.tar.gz"
ARG         LIBXML2_SHA256SUM="80efe9e6b48f8aa7b9b0c47be427e2ef2dbfb2999124220ffbc0f43ca6adb98c libxml2-v2.9.14.tar.gz"
ARG         LIBBLURAY_SHA256SUM="c24b0f41c5b737bbb65c544fe63495637a771c10a519dfc802e769f112b43b75 libbluray-1.3.1.tar.bz2"
ARG         LIBZMQ_SHA256SUM="0ff5a531c9ffaf0dfdc7dc78d13d1383088f454896d252934c429b2554d10559 v4.3.4.tar.gz"
ARG         LIBARIBB24_SHA256SUM="f61560738926e57f9173510389634d8c06cabedfa857db4b28fb7704707ff128 v1.0.3.tar.gz"

ARG         LD_LIBRARY_PATH=/opt/ffmpeg/lib
ARG         MAKEFLAGS="-j2"
ARG         PKG_CONFIG_PATH="/opt/ffmpeg/share/pkgconfig:/opt/ffmpeg/lib/pkgconfig:/opt/ffmpeg/lib64/pkgconfig"
ARG         PREFIX=/opt/ffmpeg
ARG         LD_LIBRARY_PATH="/opt/ffmpeg/lib:/opt/ffmpeg/lib64:/usr/lib64:/usr/lib:/lib64:/lib"
ENV         DEBIAN_FRONTEND=noninteractive

RUN         apt-get -yqq update
RUN         buildDeps="autoconf \
                        automake \
                        cmake \
                        curl \
                        bzip2 \
                        libexpat1-dev \
                        g++ \
                        gcc \
                        git \
                        gperf \
                        libtool \
                        make \
                        perl \
                        pkg-config \
                        python3-pip \
                        ninja-build \
                        libssl-dev \
                        checkinstall \
                        build-essential \
                        libavcodec-dev \
                        libavformat-dev \
                        libswscale-dev \
                        libdrm-dev \
                        i965-va-driver-shaders \
                        xorg \
                        xorg-dev \
                        openbox \
                        libxv1 \
                        libx11-dev \
                        libx11-xcb-dev \
                        libxcb-dri3-dev \
                        libgl1-mesa-glx \
                        libgl1-mesa-dev \
                        libwayland-dev \
                        zlib1g-dev" && \
            apt-get install -yq --no-install-recommends ${buildDeps} && \
            pip3 install --upgrade pip setuptools && \
            pip3 install meson
# nasm https://www.nasm.us/pub/nasm/releasebuilds 2.15 2020-06-27 15:37
RUN \
        DIR=/tmp/nasm && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl https://www.nasm.us/pub/nasm/releasebuilds/${NASM_VERSION}/nasm-${NASM_VERSION}.tar.bz2 | \
        tar -jx --strip-components 1 && \
        ./autogen.sh && \
        ./configure --prefix=${SRC} && \
        make -j$(nproc) && \
        make install && \
        rm -rf ${DIR}
# yasm https://www.tortall.net/projects/yasm/releases/ 1.3.0 11-Aug-2014 06:29
RUN \
        DIR=/tmp/yasm && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl https://www.tortall.net/projects/yasm/releases/yasm-${YASM_VERSION}.tar.gz | \
        tar -zx --strip-components 1 && \
        ./configure \
          --prefix=${SRC} && \
        make -j$(nproc) && \
        make install && \
        ldconfig
## opencore-amr https://sourceforge.net/projects/opencore-amr/ 0.1.5 2017-03-16
RUN \
        DIR=/tmp/opencore-amr && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sL https://versaweb.dl.sourceforge.net/project/opencore-amr/opencore-amr/opencore-amr-${OPENCOREAMR_VERSION}.tar.gz | \
        tar -zx --strip-components=1 && \
        ./configure --prefix="${PREFIX}" --enable-shared  && \
        make && \
        make install && \
        rm -rf ${DIR}

#AviSynth+ 3.7.2 18 Mar 2022
RUN    set -xe && \
        cd /usr/local/src && \
        git clone --depth 1 -b ${AVISYNTHPLUS_VERSION} https://github.com/AviSynth/AviSynthPlus.git && \
        cd AviSynthPlus && \
        mkdir avisynth-build && \
        cd avisynth-build && \
        cmake ../ -G Ninja && \
        ninja && \
        checkinstall --pkgname=avisynth --pkgversion="$(grep -r \
            Version avs_core/avisynth.pc | cut -f2 -d " ")-$(date --rfc-3339=date | \
            sed 's/-//g')-git" --backup=no --deldoc=yes --delspec=yes --deldesc=yes \
            --strip=yes --stripso=yes --addso=yes --fstrans=no --default ninja install && \
        ldconfig

# l-smash
RUN     set -xe && \
        DIR=/tmp/l-smash&& \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        git clone https://github.com/l-smash/l-smash.git && \
        cd l-smash && \
        ./configure \
          --prefix="${PREFIX}" \
          --enable-shared \
          && \
        make && \
        make install && \
        ldconfig && \
        rm -rf ${DIR}

## SVT-AV1
RUN     set -xe && \
            cd /usr/local/src && \
            git clone --depth 1 https://gitlab.com/AOMediaCodec/SVT-AV1.git && \
            cd SVT-AV1/Build && \
            cmake .. -G"Unix Makefiles" -DCMAKE_BUILD_TYPE=Release && \
            make -j $(nproc) && \
            make install

# l-smash-source
RUN     set -xe && \
        DIR=/tmp/lsmashsouce && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        git clone https://github.com/zorro901/L-SMASH-Works.git && \
        cd L-SMASH-Works/AviSynth && \
        LDFLAGS="-Wl,-Bsymbolic" meson build && \
        cd build && \
        ninja -v && \
        ninja install && \
        rm -rf ${DIR}

## x264 http://www.videolan.org/developers/x264.html x264-snapshot-20191217-2245.tar.bz2 17-Dec-2019 21:45
RUN \
        DIR=/tmp/x264 && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sL https://download.videolan.org/pub/videolan/x264/snapshots/x264-snapshot-${X264_VERSION}.tar.bz2 | \
        tar -jx --strip-components=1 && \
        ./configure --prefix="${PREFIX}" --enable-shared --enable-pic && \
        make && \
        make install && \
        rm -rf ${DIR}
### x265 http://x265.org/ 3.2.1 06-Nov-2019 21:09
RUN \
        DIR=/tmp/x265 && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sL https://download.videolan.org/pub/videolan/x265/x265_${X265_VERSION}.tar.gz  | \
        tar -zx && \
        cd x265_${X265_VERSION}/build/linux && \
        sed -i "/-DEXTRA_LIB/ s/$/ -DCMAKE_INSTALL_PREFIX=\${PREFIX}/" multilib.sh && \
        sed -i "/^cmake/ s/$/ -DENABLE_CLI=OFF/" multilib.sh && \
        ./multilib.sh && \
        make -C 8bit install && \
        rm -rf ${DIR}
### libogg https://www.xiph.org/ogg/ 1.3.5 2021-06-04 03:26
RUN \
        DIR=/tmp/ogg && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO http://downloads.xiph.org/releases/ogg/libogg-${OGG_VERSION}.tar.gz && \
        echo ${OGG_SHA256SUM} | sha256sum --check && \
        tar -zx --strip-components=1 -f libogg-${OGG_VERSION}.tar.gz && \
        ./configure --prefix="${PREFIX}" --enable-shared  && \
        make && \
        make install && \
        rm -rf ${DIR}
### libopus https://www.opus-codec.org/ 1.3.1 12-Apr-2019 23:27
RUN \
        DIR=/tmp/opus && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://archive.mozilla.org/pub/opus/opus-${OPUS_VERSION}.tar.gz && \
        echo ${OPUS_SHA256SUM} | sha256sum --check && \
        tar -zx --strip-components=1 -f opus-${OPUS_VERSION}.tar.gz && \
        autoreconf -fiv && \
        ./configure --prefix="${PREFIX}" --enable-shared && \
        make && \
        make install && \
        rm -rf ${DIR}
### libvorbis https://xiph.org/vorbis/ 1.3.7 2020-07-04 06:30
RUN \
        DIR=/tmp/vorbis && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://downloads.xiph.org/releases/vorbis/libvorbis-${VORBIS_VERSION}.tar.gz && \
        echo ${VORBIS_SHA256SUM} | sha256sum --check && \
        tar -zx --strip-components=1 -f libvorbis-${VORBIS_VERSION}.tar.gz && \
        ./configure --prefix="${PREFIX}" --with-ogg="${PREFIX}" --enable-shared && \
        make && \
        make install && \
        rm -rf ${DIR}
### libtheora http://www.theora.org/ 1.1.1 2010-01-25 14:33
RUN \
        DIR=/tmp/theora && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://downloads.xiph.org/releases/theora/libtheora-${THEORA_VERSION}.tar.gz && \
        echo ${THEORA_SHA256SUM} | sha256sum --check && \
        tar -zx --strip-components=1 -f libtheora-${THEORA_VERSION}.tar.gz && \
        ./autogen.sh && \
        sed -i 's/png_\(sizeof\)/\1/g' examples/png2theora.c && \
        ./configure --prefix="${PREFIX}" --with-ogg="${PREFIX}" --enable-shared --disable-static && \
        make && \
        make check && \
        make install && \
        rm -rf ${DIR}
### libvpx https://www.webmproject.org/code/ 1.11.0 on 8 Oct 2021
RUN \
        DIR=/tmp/vpx && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sL https://codeload.github.com/webmproject/libvpx/tar.gz/v${VPX_VERSION} | \
        tar -zx --strip-components=1 && \
        ./configure --prefix="${PREFIX}" --enable-vp8 --enable-vp9 --enable-vp9-highbitdepth --enable-pic --enable-shared \
        --disable-debug --disable-examples --disable-docs --disable-install-bins  && \
        make && \
        make install && \
        rm -rf ${DIR}
### libwebp https://developers.google.com/speed/webp/ https://storage.googleapis.com/downloads.webmproject.org/releases/webp/index.html 1.2.2 2022-01-20T02:44:24Z
RUN \
        DIR=/tmp/vebp && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sL https://storage.googleapis.com/downloads.webmproject.org/releases/webp/libwebp-${WEBP_VERSION}.tar.gz | \
        tar -zx --strip-components=1 && \
        ./configure --prefix="${PREFIX}" --enable-shared  && \
        make && \
        make install && \
        rm -rf ${DIR}
### libmp3lame http://lame.sourceforge.net/ 3.100 2017-10-13
RUN \
        DIR=/tmp/lame && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sL https://versaweb.dl.sourceforge.net/project/lame/lame/$(echo ${LAME_VERSION} | sed -e 's/[^0-9]*\([0-9]*\)[.]\([0-9]*\)[.]\([0-9]*\)\([0-9A-Za-z-]*\)/\1.\2/')/lame-${LAME_VERSION}.tar.gz | \
        tar -zx --strip-components=1 && \
        ./configure --prefix="${PREFIX}" --bindir="${PREFIX}/bin" --enable-shared --enable-nasm --disable-frontend && \
        make && \
        make install && \
        rm -rf ${DIR}
### xvid https://www.xvid.com/ https://labs.xvid.com/source/ 28/12/2019 1.3.7
RUN \
        DIR=/tmp/xvid && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://downloads.xvid.com/downloads/xvidcore-${XVID_VERSION}.tar.gz && \
        echo ${XVID_SHA256SUM} | sha256sum --check && \
        tar -zx -f xvidcore-${XVID_VERSION}.tar.gz && \
        cd xvidcore/build/generic && \
        ./configure --prefix="${PREFIX}" --bindir="${PREFIX}/bin" && \
        make && \
        make install && \
        rm -rf ${DIR}
### fdk-aac https://github.com/mstorsjo/fdk-aac 2.0.2 28 Apr 2021
RUN \
        DIR=/tmp/fdk-aac && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sL https://github.com/mstorsjo/fdk-aac/archive/v${FDKAAC_VERSION}.tar.gz | \
        tar -zx --strip-components=1 && \
        autoreconf -fiv && \
        ./configure --prefix="${PREFIX}" --enable-shared --datadir="${DIR}" && \
        make && \
        make install && \
        rm -rf ${DIR}
## openjpeg https://github.com/uclouvain/openjpeg 2.5.0 2022/5/14
RUN \
        DIR=/tmp/openjpeg && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sL https://github.com/uclouvain/openjpeg/archive/v${OPENJPEG_VERSION}.tar.gz | \
        tar -zx --strip-components=1 && \
        cmake -DBUILD_THIRDPARTY:BOOL=ON -DCMAKE_INSTALL_PREFIX="${PREFIX}" . && \
        make && \
        make install && \
        rm -rf ${DIR}
## freetype https://www.freetype.org/ 2.12.1 01-May-2022 05:55
RUN  \
        DIR=/tmp/freetype && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://download.savannah.gnu.org/releases/freetype/freetype-${FREETYPE_VERSION}.tar.gz && \
        echo ${FREETYPE_SHA256SUM} | sha256sum --check && \
        tar -zx --strip-components=1 -f freetype-${FREETYPE_VERSION}.tar.gz && \
        ./configure --prefix="${PREFIX}" --disable-static --enable-shared && \
        make && \
        make install && \
        rm -rf ${DIR}
## libvstab https://github.com/georgmartius/vid.stab 1.1.0 2017
RUN  \
        DIR=/tmp/vid.stab && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://github.com/georgmartius/vid.stab/archive/v${LIBVIDSTAB_VERSION}.tar.gz && \
        echo ${LIBVIDSTAB_SHA256SUM} | sha256sum --check &&  \
        tar -zx --strip-components=1 -f v${LIBVIDSTAB_VERSION}.tar.gz && \
        cmake -DCMAKE_INSTALL_PREFIX="${PREFIX}" . && \
        make && \
        make install && \
        rm -rf ${DIR}
## fridibi https://www.fribidi.org/ 1.0.12 20 Apr 2022
RUN  \
        DIR=/tmp/fribidi && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://github.com/fribidi/fribidi/archive/v${FRIBIDI_VERSION}.tar.gz && \
        echo ${FRIBIDI_SHA256SUM} | sha256sum --check && \
        tar -zx --strip-components=1 -f v${FRIBIDI_VERSION}.tar.gz && \
        ./autogen.sh && \
        ./configure --prefix="${PREFIX}" --disable-static --enable-shared && \
        make -j1 && \
        make install && \
        rm -rf ${DIR}
## fontconfig https://www.freedesktop.org/wiki/Software/fontconfig/ 2.14.0 2022-03-31 11:48
RUN  \
        DIR=/tmp/fontconfig && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://www.freedesktop.org/software/fontconfig/release/fontconfig-${FONTCONFIG_VERSION}.tar.gz && \
        tar -zx --strip-components=1 -f fontconfig-${FONTCONFIG_VERSION}.tar.gz && \
        ./configure --prefix="${PREFIX}" --disable-static --enable-shared && \
        make && \
        make install && \
        rm -rf ${DIR}
## harfbuzz 4.3.0 2022/5/21
RUN  \
        DIR=/tmp/harfbuzz && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://github.com/harfbuzz/harfbuzz/archive/${HARFBUZZ_VERSION}.tar.gz && \
        tar -zx --strip-components=1 -f ${HARFBUZZ_VERSION}.tar.gz && \
        ./autogen.sh && \
        make && \
        make install && \
        rm -rf ${DIR}
## libass https://github.com/libass/libass 0.16.0 2022/5/13
RUN  \
        DIR=/tmp/libass && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://github.com/libass/libass/archive/${LIBASS_VERSION}.tar.gz && \
        echo ${LIBASS_SHA256SUM} | sha256sum --check && \
        tar -zx --strip-components=1 -f ${LIBASS_VERSION}.tar.gz && \
        ./autogen.sh && \
        ./configure --prefix="${PREFIX}" --disable-static --enable-shared && \
        make && \
        make install && \
        rm -rf ${DIR}
## kvazaar https://github.com/ultravideo/kvazaar 2.1.0 13 Oct 2021
RUN \
        DIR=/tmp/kvazaar && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://github.com/ultravideo/kvazaar/archive/v${KVAZAAR_VERSION}.tar.gz && \
        tar -zx --strip-components=1 -f v${KVAZAAR_VERSION}.tar.gz && \
        ./autogen.sh && \
        ./configure --prefix="${PREFIX}" --disable-static --enable-shared && \
        make && \
        make install && \
        rm -rf ${DIR}
## Open Media https://aomedia.googlesource.com/aom/+/refs/tags/v3.3.0 Tue Feb 15 17:10:54 2022
RUN \
        DIR=/tmp/aom && \
        git clone --branch ${AOM_VERSION} --depth 1 https://aomedia.googlesource.com/aom ${DIR} ; \
        cd ${DIR} ; \
        rm -rf CMakeCache.txt CMakeFiles ; \
        mkdir -p ./aom_build ; \
        cd ./aom_build ; \
        cmake -DCMAKE_INSTALL_PREFIX="${PREFIX}" -DBUILD_SHARED_LIBS=1 ..; \
        make ; \
        make install ; \
        rm -rf ${DIR}
## libxcb (and supporting libraries) for screen capture https://xcb.freedesktop.org/ 1.19.3 2021-01-24 14:41
RUN \
        DIR=/tmp/xorg-macros && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://www.x.org/archive//individual/util/util-macros-${XORG_MACROS_VERSION}.tar.gz && \
        tar -zx --strip-components=1 -f util-macros-${XORG_MACROS_VERSION}.tar.gz && \
        ./configure --srcdir=${DIR} --prefix="${PREFIX}" && \
        make && \
        make install && \
        rm -rf ${DIR}
## xproto 7.0.31 2016-09-23 06:50
RUN \
        DIR=/tmp/xproto && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://www.x.org/archive/individual/proto/xproto-${XPROTO_VERSION}.tar.gz && \
        tar -zx --strip-components=1 -f xproto-${XPROTO_VERSION}.tar.gz && \
        ./configure --srcdir=${DIR} --prefix="${PREFIX}" && \
        make && \
        make install && \
        rm -rf ${DIR}
## libXau 1.0.9 2019-02-10 22:46
RUN \
        DIR=/tmp/libXau && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://www.x.org/archive/individual/lib/libXau-${XAU_VERSION}.tar.gz && \
        tar -zx --strip-components=1 -f libXau-${XAU_VERSION}.tar.gz && \
        ./configure --srcdir=${DIR} --prefix="${PREFIX}" && \
        make && \
        make install && \
        rm -rf ${DIR}
## libpthread-stubs 0.4 2017-03-14 17:55
RUN \
        DIR=/tmp/libpthread-stubs && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://xcb.freedesktop.org/dist/libpthread-stubs-${LIBPTHREAD_STUBS_VERSION}.tar.gz && \
        tar -zx --strip-components=1 -f libpthread-stubs-${LIBPTHREAD_STUBS_VERSION}.tar.gz && \
        ./configure --prefix="${PREFIX}" && \
        make && \
        make install && \
        rm -rf ${DIR}
## xcb-proto-1.15.tar.xz 2022-05-03 20:47
RUN \
        DIR=/tmp/libxcb-proto && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://xcb.freedesktop.org/dist/xcb-proto-${XCBPROTO_VERSION}.tar.gz && \
        tar -zx --strip-components=1 -f xcb-proto-${XCBPROTO_VERSION}.tar.gz && \
        ACLOCAL_PATH="${PREFIX}/share/aclocal" ./autogen.sh && \
        ./configure --prefix="${PREFIX}" && \
        make && \
        make install && \
        rm -rf ${DIR}
## libxcb-1.15.tar.gz 2022-05-03 22:17
RUN \
        DIR=/tmp/libxcb && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://xcb.freedesktop.org/dist/libxcb-${LIBXCB_VERSION}.tar.gz && \
        tar -zx --strip-components=1 -f libxcb-${LIBXCB_VERSION}.tar.gz && \
        ACLOCAL_PATH="${PREFIX}/share/aclocal" ./autogen.sh && \
        ./configure --prefix="${PREFIX}" --disable-static --enable-shared && \
        make && \
        make install && \
        rm -rf ${DIR}
## libxml2 - for libbluray https://gitlab.gnome.org/GNOME/libxml2/-/releases 2.9.14 2022/6/17
RUN \
        DIR=/tmp/libxml2 && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://gitlab.gnome.org/GNOME/libxml2/-/archive/v${LIBXML2_VERSION}/libxml2-v${LIBXML2_VERSION}.tar.gz && \
        echo ${LIBXML2_SHA256SUM} | sha256sum --check && \
        tar -xz --strip-components=1 -f libxml2-v${LIBXML2_VERSION}.tar.gz && \
        ./autogen.sh --prefix="${PREFIX}" --with-ftp=no --with-http=no --with-python=no && \
        make && \
        make install && \
        rm -rf ${DIR}
## libbluray - Requires libxml, freetype, and fontconfig libbluray-1.3.1.tar.bz2 03-Mar-2022 17:47
RUN \
        DIR=/tmp/libbluray && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://download.videolan.org/pub/videolan/libbluray/${LIBBLURAY_VERSION}/libbluray-${LIBBLURAY_VERSION}.tar.bz2 && \
        echo ${LIBBLURAY_SHA256SUM} | sha256sum --check && \
        tar -jx --strip-components=1 -f libbluray-${LIBBLURAY_VERSION}.tar.bz2 && \
        ./configure --prefix="${PREFIX}" --disable-examples --disable-bdjava-jar --disable-static --enable-shared && \
        make && \
        make install && \
        rm -rf ${DIR}
## libzmq https://github.com/zeromq/libzmq/ 4.3.4 17 Jan 2021
RUN \
        DIR=/tmp/libzmq && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://github.com/zeromq/libzmq/archive/v${LIBZMQ_VERSION}.tar.gz && \
        echo ${LIBZMQ_SHA256SUM} | sha256sum --check && \
        tar -xz --strip-components=1 -f v${LIBZMQ_VERSION}.tar.gz && \
        ./autogen.sh && \
        ./configure --prefix="${PREFIX}" && \
        make && \
#        make check && \
        make install && \
        rm -rf ${DIR}
## libsrt https://github.com/Haivision/srt 1.4.4 04 Oct 2021
RUN \
        DIR=/tmp/srt && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://github.com/Haivision/srt/archive/v${LIBSRT_VERSION}.tar.gz && \
        tar -xz --strip-components=1 -f v${LIBSRT_VERSION}.tar.gz && \
        cmake -DCMAKE_INSTALL_PREFIX="${PREFIX}" . && \
        make && \
        make install && \
        rm -rf ${DIR}
## libpng 1.6.37 2019-04-14
RUN \
        DIR=/tmp/png && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        git clone https://git.code.sf.net/p/libpng/code ${DIR} -b v${LIBPNG_VERSION} --depth 1 && \
        ./configure --prefix="${PREFIX}" && \
        make check && \
        make install && \
        rm -rf ${DIR}
## libaribb24 1.0.3 19 Aug 2014
RUN \
        DIR=/tmp/b24 && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        curl -sLO https://github.com/nkoriyama/aribb24/archive/v${LIBARIBB24_VERSION}.tar.gz && \
        echo ${LIBARIBB24_SHA256SUM} | sha256sum --check && \
        tar -xz --strip-components=1 -f v${LIBARIBB24_VERSION}.tar.gz && \
        autoreconf -fiv && \
        ./configure CFLAGS="-I${PREFIX}/include -fPIC" --prefix="${PREFIX}" && \
        make && \
        make install && \
        rm -rf ${DIR}
RUN \
    DIR=/tmp/libva && \
    mkdir -p ${DIR} && \
    cd ${DIR} && \
    git clone https://github.com/intel/libva && \
    cd libva && \
    ./autogen.sh && \
    ./configure && \
    make -j$(nproc) VERBOSE=1 && \
    make -j$(nproc) install && \
    rm -rf ${DIR}
RUN \
    DIR=/tmp/cmrt && \
    mkdir -p ${DIR} && \
    cd ${DIR} && \
    git clone https://github.com/intel/cmrt && \
    cd cmrt && \
    ./autogen.sh && \
    ./configure && \
    make -j$(nproc) VERBOSE=1 && \
    make -j$(nproc) install && \
    rm -rf ${DIR}
RUN \
    DIR=/tmp/intel-vaapi-driver && \
    mkdir -p ${DIR} && \
    cd ${DIR} && \
    git clone https://github.com/intel/intel-vaapi-driver && \
    cd intel-vaapi-driver && \
    ./autogen.sh && \
    ./configure && \
    make -j$(nproc) VERBOSE=1 && \
    make -j$(nproc) install && \
    rm -rf ${DIR}
RUN \
    DIR=/tmp/libva-utils && \
    mkdir -p ${DIR} && \
    cd ${DIR} && \
    git clone https://github.com/intel/libva-utils && \
    cd libva-utils && \
    ./autogen.sh && \
    ./configure && \
    make -j$(nproc) VERBOSE=1 && \
    make -j$(nproc) install && \
    rm -rf ${DIR}
# gmmlibのインストール
RUN cd /tmp && \
        git clone https://github.com/intel/gmmlib && \
        cd gmmlib && \
        mkdir build && cd build && \
        cmake -DCMAKE_BUILD_TYPE= Release -DARCH=64 ../ && \
        make && \
        make install
# Intel-Media-Driverのインストール
RUN cd /tmp && \
        git clone https://github.com/intel/media-driver && \
        mkdir build_media && cd build_media && \
        cmake ../media-driver && \
        make -j"$(nproc)" && \
        make install
# Intel-Media-Driverで生成されたライブラリをffmpegで使用するために移動
RUN cd /tmp && \
    mkdir -p /usr/local/lib/dri && \
    cp /tmp/build_media/media_driver/iHD_drv_video.so /usr/local/lib/dri/
# Intel-Media-SDKのインストール
RUN cd /tmp && \
        git clone https://github.com/Intel-Media-SDK/MediaSDK msdk && \
        cd msdk && \
        git submodule init && \
        git pull && \
        mkdir -p /tmp/build_msdk && cd /tmp/build_msdk && \
        cmake -DCMAKE_BUILD_TYPE=Release -DENABLE_WAYLAND=ON -DENABLE_X11_DRI3=ON -DENABLE_OPENCL=ON  ../msdk && \
        make && \
        make install && \
        echo '/opt/intel/mediasdk/lib' > /etc/ld.so.conf.d/imsdk.conf && \
        exit && \
        ldconfig
## ffmpeg https://ffmpeg.org/
RUN  \
        DIR=/tmp && mkdir -p ${DIR} && cd ${DIR} && \
        git clone --depth 1 -b ${FFMPEG_VERSION} git://git.ffmpeg.org/ffmpeg.git && \
        DIR=/tmp/ffmpeg && mkdir -p ${DIR} && cd ${DIR} && \
        ldconfig && \
        ./configure \
        --disable-debug \
        --disable-doc \
        --disable-ffplay \
        --enable-shared \
        --enable-libopencore-amrnb \
        --enable-libopencore-amrwb \
        --enable-gpl \
        --enable-libass \
        --enable-fontconfig \
        --enable-libfreetype \
        --enable-libvidstab \
        --enable-libmp3lame \
        --enable-libopus \
        --enable-libtheora \
        --enable-libvorbis \
        --enable-libvpx \
        --enable-libwebp \
        --enable-libxcb \
        --enable-libx265 \
        --enable-libxvid \
        --enable-libx264 \
        --enable-libfdk-aac \
        --enable-libsvtav1 \
        --enable-nonfree \
        --enable-openssl \
        --enable-libfdk_aac \
        --enable-postproc \
        --enable-small \
        --enable-version3 \
        --enable-libbluray \
        --enable-libzmq \
        --extra-libs=-ldl \
        --prefix="${PREFIX}" \
        --enable-libopenjpeg \
        --enable-libkvazaar \
        --enable-libaom \
        --enable-avisynth \
        --extra-libs=-lpthread \
        --enable-libsrt \
        --enable-libaribb24 \
        --enable-debug=3 \
        --enable-vaapi \
        --extra-cflags="-I/opt/intel/mediasdk/include" \
        --extra-ldflags="-L/opt/intel/mediasdk/lib" \
        --extra-ldflags="-L/opt/intel/mediasdk/plugins" \
        --extra-cflags="-I${PREFIX}/include" \
        --extra-ldflags="-L${PREFIX}/lib" && \
        make -j`nproc` && \
        make install && \
        make tools/zmqsend && cp tools/zmqsend ${PREFIX}/bin/ && \
        make distclean && \
        hash -r && \
        cd tools && \
        make qt-faststart && cp qt-faststart ${PREFIX}/bin/

#FFMS2 2.40 22 Aug 2020
RUN     set -xe && \
        DIR=/tmp/ffms2 && \
        mkdir -p ${DIR} && \
        cd ${DIR} && \
        git clone --depth 1 https://github.com/ffms/ffms2.git && \
        cd ffms2 && \
        PKG_CONFIG_PATH=${PREFIX}/lib/pkgconfig \
        CPPFLAGS="-I${SRC}/include/avisynth" \
        ./autogen.sh --enable-shared --enable-avisynth && \
        make -j$(nproc) && \
        make install && \
        rm -rf ${DIR}
RUN cp /usr/lib/x86_64-linux-gnu/libXv.so.1 /usr/local/lib/
RUN cp /usr/lib/x86_64-linux-gnu/libXv.so.1.0.0 /usr/local/lib/
RUN cp /usr/lib/x86_64-linux-gnu/libX11.so.6 /usr/local/lib/
RUN cp /usr/lib/x86_64-linux-gnu/libXext.so.6 /usr/local/lib/
RUN cp /usr/lib/x86_64-linux-gnu/libdrm.so.2 /usr/local/lib/
RUN cp /usr/lib/x86_64-linux-gnu/libXfixes.so.3 /usr/local/lib/
RUN cp /usr/lib/x86_64-linux-gnu/libXdmcp.so.6 /usr/local/lib/
RUN cp /usr/lib/x86_64-linux-gnu/libbrotlidec.so.1 /usr/local/lib/
RUN cp /usr/lib/x86_64-linux-gnu/libbsd.so.0 /usr/local/lib/
RUN cp /usr/lib/x86_64-linux-gnu/libbrotlicommon.so.1 /usr/local/lib/
RUN cp /usr/lib/x86_64-linux-gnu/libmd.so.0 /usr/local/lib/
# cleanup
RUN \
        ldd ${PREFIX}/bin/ffmpeg | grep opt/ffmpeg | cut -d ' ' -f 3 | xargs -i cp {} /usr/local/lib/ && \
        ldd ${SRC}/lib/avisynth/liblsmashsource.so | grep opt/ffmpeg | cut -d ' ' -f 3 | xargs -i cp {} /usr/local/lib/ && \
        cp ${PREFIX}/bin/* /usr/local/bin/ && \
        cp -r ${PREFIX}/share/ffmpeg /usr/local/share/ && \
        LD_LIBRARY_PATH=/usr/local/lib ffmpeg -buildconf

# release image
FROM        base AS release
MAINTAINER  zorro901 <zoro907@gmail.com>
ENV         LD_LIBRARY_PATH=/usr/local/lib:/usr/local/lib64:/usr/lib:/usr/lib64:/lib:/lib64
COPY        --from=build /usr/local /usr/local
CMD         ["--help"]
ENTRYPOINT  ["ffmpeg"]