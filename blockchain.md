# Blockchain poc usage

Adding a new transaction
```bash
curl \
    -s \
	-H "Content-Type: application/json" \
	-d '{
            "sender": "bob",
            "recipient": "alice",
            "amount": 5
        }' \
    http://localhost:5000/transactions/new |\
jq .
```

Mining a new block, miner will be payed 1
```bash
curl -s http://localhost:5000/mine |jq .
```

Register a new node in the network
```bash
curl \
    -s \
	-H "Content-Type: application/json" \
	-d '{
           "nodes": ["http://localhost:5001"]
        }' \
    http://localhost:5000/nodes/register |\
jq .
```

And register the old node in the new one
```bash
curl \
    -s \
	-H "Content-Type: application/json" \
	-d '{
           "nodes": ["http://localhost:5000"]
        }' \
    http://localhost:5001/nodes/register |\
jq .
```

Resolving blockchain differences in each nodes
```bash
curl -s http://localhost:5000/nodes/resolve |jq .
```
```bash
curl -s http://localhost:5001/nodes/resolve |jq .
```

Requesting the blockchain of a node
```bash
curl -s http://localhost:5000/chain |jq .
```
```bash
curl -s http://localhost:5001/chain |jq .
```

