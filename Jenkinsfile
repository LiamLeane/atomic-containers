podTemplate(label: 'dockerbuild', nodeSelector: 'beta.kubernetes.io/os=linux', containers: [		
			containerTemplate(name: 'docker', image: 'docker', ttyEnabled: true, command: 'cat'),
			containerTemplate(name: 'jnlp', image: 'citrixclientvirtualizationbuild.azurecr.io/jenkinslinux:fabricpath', args: '${computer.jnlpmac} ${computer.name}')
	], volumes: [hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock')]) {
	node('dockerbuild')
	{		
		def tag = ""		
		def registry = "appopsos.azurecr.io"
		
		stage ("Git")
		{
			def scmparam = checkout(scm)
			tag = scmparam.GIT_BRANCH.split("/").last()
			if (tag == "master")
			{
				tag = "latest"
			}
		}
		
		container('docker')
		{
			buildAndPublish('virtualagent-xenserver', registry, tag)
			buildAndPublish('virtualagent-vmware', registry, tag)
			buildAndPublish('virtualagent-nutanix', registry, tag)
			//buildAndPublish('virtualagent-hyperv', registry, tag)
			//buildAndPublish('virtualagent-azure', registry, tag)
			
			buildAndPublish('kube-base', registry, tag)
			buildAndPublish('kube-master', registry, tag)
			buildAndPublish('kube-apiserver', registry, tag)
			buildAndPublish('kube-controller-manager', registry, tag)
			buildAndPublish('kube-kubeadm', registry, tag)
			buildAndPublish('kube-node', registry, tag)
			buildAndPublish('kube-kubelet', registry, tag)
			buildAndPublish('kube-proxy', registry, tag)
			buildAndPublish('kube-scheduler', registry, tag)
		}
	}
}

def buildAndPublish(String folder, String registry, String tag, Map arguments = null)
{
    def params = (arguments?.collect{ k,v-> "$k=$v" })?.join(',')
    def args = params?(("--build-arg ".concat("${params}")))<<" " : ""
    stage(folder)
    {
        withCredentials(
            [
                [
                    $class: 'UsernamePasswordMultiBinding',
                    credentialsId: 'docker-os-credentials',
                    usernameVariable: 'DOCKER_USERNAME',
                    passwordVariable: 'DOCKER_PASSWORD'
                ]
            ]
        )
        {            
			sh("docker login ${registry} -u ${env.DOCKER_USERNAME} -p ${env.DOCKER_PASSWORD}")
			sh("docker build ${args}${folder} -t ${registry}/${folder}:${tag}")
			sh("docker push ${registry}/${folder}:${tag}")            
        }
    }
}