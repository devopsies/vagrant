provisionPath = "init.sh"

nodes = [
	{:hostname => "web-server", :cpus => 1, :mem => 512, :provisionScript => provisionPath}
]


Vagrant.configure(2) do |config|
	nodes.each do |node|
		config.vm.define node[:hostname] do |vmachine|
			vmachine.vm.box_download_insecure = true
			vmachine.vm.box = "ubuntu/focal64"
			vmachine.vm.box_check_update = false
			vmachine.vm.hostname = node[:hostname]
			vmachine.vm.provider :virtualbox do |domain|
				domain.memory = node[:mem]
				domain.cpus = node[:cpus]
			end
			vmachine.vm.provision :file, source: "index.html", destination: "/etc/nginx/html/index.html"
			vmachine.vm.provision :shell, path: node[:provisionScript]
			vmachine.vm.network "forwarded_port", guest: 80, host: 8080
		end
	end
end
