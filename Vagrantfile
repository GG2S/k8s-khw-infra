
Vagrant.configure("2") do |config|
	# vm의 OS 버전
	config.vm.box = "rockylinux/8"
	
	# 자동 box 버전 업데이트 설정 해제 (defualt : true)
	config.vm.box_check_update = false
	
	# VMware shared folder 문제 예방용
	config.vm.synced_folder ".", "/vagrant", disabled: true
	
	# master node 지정
	config.vm.define "master" do |master|
		
		# vm의 host 이름
		master.vm.hostname = "k8s-master-khw"
	
		# 포트 포워딩 Host 8080 -> Guest 80
		master.vm.network "forwarded_port",
			guest: 22,
			host: 2222,
			id: "ssh"
		# 사설 네트워크 ip 번호 부여
		master.vm.network "private_network",
			ip: "192.168.77.30"
	
		# vmware의 전용 옵션
		# vm의 memory, cpu 설정
		master.vm.provider "vmware_desktop" do |v|
			v.vmx["memsize"] = "6144"
			v.vmx["numvcpus"] = "4"
		end
		s
		# shell 스크립트 실행
		config.vm.provision "shell",
			inline: "echo hello master"
	end
	
	# worker node 지정
	config.vm.define "worker1" do |worker|
		
		# vm의 host 이름
		worker.vm.hostname = "k8s-worker1-khw"
	
		# 포트 포워딩 Host 8081 -> Guest 81
		worker.vm.network "forwarded_port",
			guest: 22,
			host: 2223,
			id: "ssh"
		# 사설 네트워크 ip 번호 부여
		worker.vm.network "private_network",
			ip: "192.168.77.31"
	
		# vmware의 전용 옵션
		# vm의 memory, cpu 설정
		worker.vm.provider "vmware_desktop" do |v|
			v.vmx["memsize"] = "6144"
			v.vmx["numvcpus"] = "4"
		end
		
		# shell 스크립트 실행
		config.vm.provision "shell",
			inline: "echo hello worker1"
	end
end