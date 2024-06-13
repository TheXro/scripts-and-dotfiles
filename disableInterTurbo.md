# Disable turbo Mode in intel CPUs 

  - First make the service file
    
    ```
    sudo nano /etc/systemd/system/disable_turbo_boost.service
    ```
  - Paste the following Code
    ```
    [Unit]
    Description=Disable Turbo Boost

    [Service]
    Type=oneshot
    ExecStart=/bin/sh -c 'echo 1 > /sys/devices/system/cpu/intel_pstate/no_turbo'
    RemainAfterExit=true

    [Install]
    WantedBy=multi-user.target
    ```
- Enable the service
  ```
  sudo systemctl enable disable_turbo_boost.service
  ```
  The output should be like this:
  ```
  Created symlink /etc/systemd/system/multi-user.target.wants/disable_turbo_boost.service →
  /etc/systemd/system/disable_turbo_boost.service.
  ```
- Start the service
  ```
  sudo systemctl start disable_turbo_boost.service
  ```
- Check if it worked or not by running `cat /sys/devices/system/cpu/intel_pstate/no_turbo`, it should give `1`.



  
