git clone --recursive https://github.com/HansKristian-Work/vkd3d-proton ~/dxvk-proton && \
cd ~/dxvk-proton && \
./package-release.sh master ./ --no-package && \
cd ~/dxvk-proton/vkd3d-proton-master && chmod +x ./setup_vkd3d_proton.sh && ./setup_vkd3d_proton.sh install
