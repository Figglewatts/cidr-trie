# cidr-trie
Store CIDR IP addresses (both v4 and v6) in a trie for easy lookup.

## Usage
```python
from cidr_trie import PatriciaTrie

# --- supports IPv4 ---
trie = PatriciaTrie()
trie.insert("0.0.0.0/0", "Internet")
trie.insert("32.0.0.0/9", "RIR-A")
trie.insert("32.128.0.0/9", "RIR-B")
trie.insert("32.32.0.0/16", "another")
trie.insert("32.32.32.0/24", "third")
trie.insert("32.32.32.32/32", "you")
trie.insert("192.168.0.1/32", "totally different")
trie.insert("33.0.0.0/8", "RIR3")
trie.insert("64.0.0.0/8", "RIR2")

# returns: ['Internet', 'RIR-A', 'another', 'third', 'you']
trie.find_all("32.32.32.32")

# returns: ['Internet', 'totally different']
trie.find_all("192.168.0.1/32")

# returns: ['Internet', 'RIR-B']
trie.find_all("32.192.0.0/10")

# --- supports IPv6 ---
trie = PatriciaTrie()
trie.insert("::/0", "Internet")
trie.insert("1234::/16", "Test")
trie.insert("1234:1001::/32", "Another one")
trie.insert("1234:1001:1920::/48", "A third")
trie.insert("1234:1001:1920:2000:2020::/96", "A fourth")
trie.insert("1234:1001:1920::ffff", "A different one")

# returns: ['Internet', 'Test', 'Another one', 'A third', 'A fourth']
trie.find_all("1234:1001:1920:2000:2020::/128")

# returns: ['Internet', 'Test', 'Another one', 'A third', 'A different one']
trie.find_all("1234:1001:1920::ffff")
```
