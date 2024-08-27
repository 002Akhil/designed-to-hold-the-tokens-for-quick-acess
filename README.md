# designed-to-hold-the-tokens-for-quick-acess
from collections import deque

class TokenCache:
    def _init_(self, max_size):
        self.max_size = max_size
        self.cache = {}
        self.order = deque()

    def getToken(self, token_key):
        return self.cache.get(token_key, None)

    def setToken(self, token_key, token_value):
        if token_key in self.cache:
            self.order.remove(token_key)
        elif len(self.order) >= self.max_size:
            oldest_key = self.order.popleft()
            del self.cache[oldest_key]

        self.order.append(token_key)
        self.cache[token_key] = token_value
        
cache = TokenCache(max_size=3)
cache.setToken("token1", "value1")
cache.setToken("token2", "value2")
cache.setToken("token3", "value3")

print(cache.getToken("token1"))  
cache.setToken("token4", "value4")  

print(cache.getToken("token1"))  
print(cache.getToken("token2"))  
