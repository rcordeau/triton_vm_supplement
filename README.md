Triton VM
---------
Ubuntu 14.04 LTS - 32-bit
	INSTALL

		sudo apt-get udpate
		sudo apt-get upgrade
		sudo apt-get dist-upgrade
		reboot
		mount Guest Additions CD and install VirtualBox guest additions
		enable shared clipboard and drag-and-drop
		sudo apt-get install git u-boot-tools ncurses-dev
		mkdir repos; cd repos; git clone https://github.com/renesas-rz/rskrza1_bsp.git
	
	SETUP/BUILD
		This sectionis adapted from the User Guide doc in the Renesas BSP repo located here: https://github.com/renesas-rz/rskrza1_bsp/blob/master/doc/User_Guide.html
		cd rskrza1_bsp/output (if not there, mkdir rskrza1_bsp/output)

			git clone https://github.com/renesas-rz/linux-3.14.git
			git clone https://github.com/renesas-rz/u-boot-2015.01.git
			cd ..

		$ ./build.sh u-boot genmai_defconfig
		$ ./build.sh u-boot
 	

		$ ./build.sh kernel genmai_xip_sdram_triton_defconfig   
				NOTE: THIS FILE EXISTS IN THE output/linux_3.14/arch/arm/configs DIRECTORY OF THE VM IMAGE, NOT THE RENESAS REPO
		$ ./build.sh kernel xipImage
		$ ./build.sh kernel dtbs
		
		$ ./build.sh buildroot triton_defconfig
		$ ./build.sh buildroot    
			NOTE: THIS FILE LIVES IN THE output/buildroot-2014.05/configs DIRECTORY OF THE VM IMAGE, NOT THE RENESAS REPO
			- select option 1 for using pre-built toolchain -- NOTE: WE *DO NOT* WANT TO USE uClibC - it will mess upwith the 	JVM build for ARM
		$ ./build.sh axfs
	