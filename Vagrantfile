VAGRANTFILE_API_VERSION = '2'

ANSIBLE_VERSION = "2.9.13"

ANSIBLE_ROLE = 'ansible-role-consul'

EPEL_REPO_8 = '''
[epel]
name     = EPEL 8 - \$basearch
baseurl  = http://mirror.globo.com/epel/8/\$basearch
enabled  = 1
gpgcheck = 0
'''

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.provider :virtualbox do |vb|
    vb.gui = false
    vb.customize [ 'modifyvm', :id, '--memory', '512' ]
    vb.customize [ 'modifyvm', :id, '--nictype1', 'virtio' ]
    vb.customize [ 'modifyvm', :id, '--natdnshostresolver1', 'on' ]
    vb.customize [ 'modifyvm', :id, '--natdnsproxy1', 'on' ]
  end
      
  config.vm.define 'ubuntu-focal' do |ubuntu_f|
    ubuntu_f.vm.box      = 'ubuntu/focal64'
    
    ubuntu_f.vm.provision 'shell', inline: 'apt-get update'
    ubuntu_f.vm.provision 'shell', inline: 'apt-get install -y -qq  python-pip libffi-dev libssl-dev python-dev'
    ubuntu_f.vm.provision 'shell', inline: "pip install -q ansible==#{ANSIBLE_VERSION} jinja2"
    ubuntu_f.vm.provision 'shell', inline: "ln -sf /vagrant /vagrant/#{ANSIBLE_ROLE}"

    ubuntu_f.vm.provision 'ansible_local' do |ansible| 
      ansible.playbook = 'tests/test_vagrant.yml'
    end
    
  end

  config.vm.define 'ubuntu-bionic' do |ubuntu_b|
    ubuntu_b.vm.box      = 'ubuntu/bionic64'
    ubuntu_b.vm.hostname = 'ubuntu-bionic'
    
    ubuntu_b.vm.provision 'shell', inline: 'apt-get update'
    ubuntu_b.vm.provision 'shell', inline: 'apt-get install -y -qq  python-pip libffi-dev libssl-dev python-dev'
    ubuntu_b.vm.provision 'shell', inline: "pip install -q ansible==#{ANSIBLE_VERSION} ansible-lint jinja2"
    ubuntu_b.vm.provision 'shell', inline: "ln -sf /vagrant /vagrant/#{ANSIBLE_ROLE}"

    ubuntu_b.vm.provision 'ansible_local' do |ansible| 
      ansible.playbook = 'tests/test_vagrant.yml'
      ansible.extra_vars = {
      }
    end
    
  end

  config.vm.define 'centos-8' do |centos8|
    centos8.vm.box      = 'centos/8'
    centos8.vm.hostname = 'centos-8'

    centos8.vm.provision 'shell', inline: 'yum install -y ca-certificates'
    centos8.vm.provision 'shell', inline: "echo \"#{EPEL_REPO_8}\" > /etc/yum.repos.d/epel.repo"
    centos8.vm.provision 'shell', inline: 'yum install -y python-pip python-devel gcc libffi-devel openssl-devel'
    centos8.vm.provision 'shell', inline: "pip install -q pip --upgrade"
    centos8.vm.provision 'shell', inline: "pip install -q ansible==#{ANSIBLE_VERSION} ansible-lint jinja2"
    centos8.vm.provision 'shell', inline: "ln -sf /vagrant /vagrant/#{ANSIBLE_ROLE}"

    centos8.vm.provision 'ansible_local' do |ansible| 
      ansible.playbook = 'tests/test_vagrant.yml'
      ansible.extra_vars = {
      }
    end
  end

end
  
# vi:ts=2:sw=2:et:ft=ruby:
