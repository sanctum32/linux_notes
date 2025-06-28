sudo dnf install meson x86_64-w64-mingw32-gcc x86_64-w64-mingw32-g++ x86_64-w64-mingw32-widl glslang.x86_64 glslang.x86_64 mingw64-glslang.noarch mingw64-glslang.noarch

git clone --recursive https://github.com/HansKristian-Work/vkd3d-proton ~/dxvk-proton && \
cd ~/dxvk-proton && \
./package-release.sh master ./ --no-package && \
cd ~/dxvk-proton/vkd3d-proton-master && chmod +x ./setup_vkd3d_proton.sh && ./setup_vkd3d_proton.sh install
