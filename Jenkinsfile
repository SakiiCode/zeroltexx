node('master') {
    timestamps {
        withEnv([
            'DEVICE=zeroltexx',
            'BRANCH=lineage-17.1',
            'VERSION=17.1',
            'ROMTYPE=UNOFFICIAL',
            'OTA_ROMTYPE=unofficial',
            'SYSTEM_PATH=/home/s4k11/dev/lineageos/zeroltexx',
            'OUTPUT_PATH=/home/s4k11/dev/lineageos/zeroltexx/out/target/product',
            'OUT=/home/s4k11/dev/lineageos/zeroltexx/out',            
            'URL=https://localhost',
            'SSH_URL=localhost',
            'LOCAL_MANIFESTS_URL=https://raw.githubusercontent.com/los-legacy/local_manifests/lineage-17.1/zero.xml',
            'LOCAL_MANIFESTS_PATH=.repo/local_manifests', 
            ]) {
            stage('Preparation') { // for display purposes
            
                checkout([$class: 'GitSCM', 
                branches: [[name: "$BRANCH"]], 
                doGenerateSubmoduleConfigurations: false, 
                extensions: [[$class: 'CleanBeforeCheckout', 
                deleteUntrackedNestedRepositories: true], 
                [$class: 'RelativeTargetDirectory', relativeTargetDir: '/home/s4k11/dev/lineageos/zeroltexx/build_script']], 
                submoduleCfg: [], 
                userRemoteConfigs: [[credentialsId: 'e1791597-2cce-40b2-8357-fcbc77a559d5', 
                url: "https://github.com/los-legacy/${DEVICE}.git"]]
                ])
                sh label: 'Preparation', script: 'bash $SYSTEM_PATH/build_script/preparation.sh'
            }
            stage('RepoSync') { // for display purposes
                sh label: 'RepoSync', script: 'bash $SYSTEM_PATH/build_script/reposync.sh'
            }
            stage('Build') { // for display purposes
                sh label: 'Build', script: 'bash $SYSTEM_PATH/build_script/build.sh'
            }
            stage('OTA Upload') { // for display purposes
                sh label: 'OTA Upload', script: 'bash $SYSTEM_PATH/build_script/upload.sh'
            }
        }
    }
}
