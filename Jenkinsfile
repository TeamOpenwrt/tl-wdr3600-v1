node('ben') {
    timestamps {
        withEnv([
            'DEVICE=tl-wdr3600-v1',
            'BRANCH=openwrt-19.07',
            'ROOT_DIR=home/benlue/openwrt',
            'OPENWRT_CONFIG_DIR=files/etc/config',
            'SCRIPT_DIR=home/benlue/openwrt/build_script',
            'OUTPUT_PATH=home/benlue/openwrt/out/target/product',
            ]) {
        
            stage('OpenWRT Preparation') {
                checkout([$class: 'GitSCM', branches: [[name: "$BRANCH"]], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'CleanBeforeCheckout'], [$class: 'RelativeTargetDirectory', relativeTargetDir: "/$ROOT_DIR"]], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/openwrt/openwrt.git']]])
            }
            stage('DEVICE Preparation') { // for display purposes
                checkout([$class: 'GitSCM', branches: [[name: "$BRANCH"]], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'CleanBeforeCheckout'], [$class: 'RelativeTargetDirectory', relativeTargetDir: "/$ROOT_DIR/build_script"]], submoduleCfg: [], userRemoteConfigs: [[url: "https://github.com/TeamOpenwrt/${DEVICE}.git"]]])
            }
            stage('Build') { // for display purposes
                sh label: 'Build', script: 'source /$SCRIPT_DIR/build.sh'
            }
            stage('OTA Upload') { // for display purposes
                //sh label: 'OTA Upload', script: 'source $SYSTEM_PATH/build_script/upload.sh'
            }
        }
    }
}
