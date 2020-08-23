# Hyperledger Fabric network setup with 3 Peer, 1 Orderer with Prometheus and Grafana  

Pre Requisite - Hyperledger Binaries and HLF Pre-Requisites software are installed

# Following are the steps to run the setup
1. create a working folder, change directory to working folder
2. git clone https://github.com/ashwanihlf/sample_monitoring.git
3. sudo chmod -R 755 sample_monitoring/
4. cd sample_monitoring  
5. mkdir config  
	<remove config and crypto-config if they are existing before creation of config folder (Optional)>
	5a. sudo rm -rf config
	5b  sudo rm -rf crypto-config
6. export COMPOSE_PROJECT_NAME=net
7. sudo ./generate.sh
8. sudo ./start.sh
9. docker exec -it cli /bin/bash
10. peer chaincode invoke -C mychannel -n samplecc -c '{"function":"initCar","Args":["Ashwani","Blue","BMW"]}'
11. peer chaincode query -C mychannel -n samplecc -c '{"function":"readCar","Args":["Ashwani"]}'      

>> returns {"color":"bmw","docType":"Car","model":"blue","owner":"Ashwani"}

12. docker exec -e "CORE_PEER_ADDRESS=peer0.org2.example.com:7051" -e "CORE_PEER_LOCALMSPID=Org2MSP" -e "CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.example.com/users/Admin@org2.example.com/msp" cli peer chaincode query -C mychannel -n samplecc -c '{"function":"readCar","Args":["Ashwani"]}'      

>> returns {"color":"bmw","docType":"Car","model":"blue","owner":"Ashwani"}

