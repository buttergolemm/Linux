# Linux Bootstrap

## bash
''''
># force color prompt
sed -i 's/#force_color_prompt=yes/force_color_prompt=yes/g' ~/.bashrc

>echo "# quick folder view: list folders + files, human readable!" | tee -a ~/.bashrc
echo "alias l='ls -lh --group-directories-first'" | tee -a ~/.bashrc

>source ~/.bashrc

># copy .bashrc to root
sudo cp ~/.bashrc /root/.bashrc
># red prompt for root user
sudo sed -i 's/;32m/;31m/g' /root/.bashrc

># sudo without password
echo "$USER ALL=(ALL) NOPASSWD:ALL" | sudo tee -a /etc/sudoers
''''
