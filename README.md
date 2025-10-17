kas shell kas-project-config.yml 
devtool modify baremetal-helloworld
bitbake -c build baremetal-helloworld
runqemu nographic slirp