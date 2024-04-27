## [ NOTICE ] The Sources are outdated!!!

### Type this command at CLI

- 1.  npm install ganache-cli web3@0.20.1 solc
- 2.  node_modules/.bin/ganache-cli

### Expected Output

- Should starts with
- Ganache CLI v6.12.2 (ganache-core: 2.13.2)
  <br/>Available Accounts ...

### The thing to do after complete write your contract (which is filename ends with .sol)

#### First - compile your code

In the node console

> code = fs.readFileSync('Voting.sol').toString()
> solc = require('solc')
> compiledCode = solc.compile(code)

#### Second - deploy your contract on blockchain

> Web3 = require('web3')
> web3 = new Web3(new Web3.providers.HttpProvider("http://localhost:8545"));
> abiDefinition = JSON.parse(compiledCode.contracts[':Voting'].interface)
> VotingContract = web3.eth.contract(abiDefinition)
> byteCode = compiledCode.contracts[':Voting'].bytecode
> deployedContract = VotingContract.new(['Rama','Nick','Jose'],{data: byteCode, from: web3.eth.accounts[0], gas: 4700000})
> deployedContract.address
> '0x0396d2b97871144f75ba9a9c8ae12bf6c019f610' <- Your address will be different

#### Third - Interaction with your deployed contract

> deployedContract.totalVotesFor.call('Rama')
> { [String: '0'] s: 1, e: 0, c: [ 0 ] }
> deployedContract.voteForCandidate('Rama', {from: web3.eth.accounts[0]})
> '0xdedc7ae544c3dde74ab5a0b07422c5a51b5240603d31074f5b75c0ebc786bf53'
> deployedContract.voteForCandidate('Rama', {from: web3.eth.accounts[0]})
> '0x02c054d238038d68b65d55770fabfca592a5cf6590229ab91bbe7cd72da46de9'
> deployedContract.voteForCandidate('Rama', {from: web3.eth.accounts[0]})
> '0x3da069a09577514f2baaa11bc3015a16edf26aad28dffbcd126bde2e71f2b76f'
> deployedContract.totalVotesFor.call('Rama').toLocaleString()
> '3'
