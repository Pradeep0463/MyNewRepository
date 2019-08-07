def checkoutGitRepository(path, url, branch, credentialsId = null, poll = true, timeout = 10, depth = 0){
    dir(path) {
        checkout(
            changelog:true,
            poll: poll,
            scm: [
                $class: 'GitSCM',
                branches: [[name: "*/${MyNewBranch}"]],
            doGenerateSubmoduleConfigurations: false,
            extensions: [
                [$class: 'CheckoutOption', timeout: timeout],
                [$class: 'CloneOption', depth: depth, noTags: false, reference: '', shallow: depth > 0, timeout: timeout]],
            submoduleCfg: [],
            userRemoteConfigs: [[url: 'https://github.com/Pradeep0463/MyNewRepository.git', credentialsId: credentialsId]]]
        )
        sh(returnStdout: true, script: 'git rev-parse HEAD').trim()
    }
}
