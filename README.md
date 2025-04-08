# humhongekamyab
______________________________________________________________________Q1________________________________________________________________________
# Generation of Simple Hash Table with Collision
class HashTable:
    def __init__(self, size):
        self.size = size
        # self.table = [None] * size  # Empty hash table
        self.table = [[] for _ in range(size)]
        # Using separate chaining for collision handling

    def hash_function(self, key):
        """Simple hash function using modulo operation"""
        return key % self.size

    def insert(self, key, value):
        """Insert key-value pair into the hash table"""
        index = self.hash_function(key)
        self.table[index].append((key, value))
        # Append to handle collisions (Separate Chaining)
        print(f"Inserted ({key}, {value}) at index {index}")

    def display(self):
        """Display the hash table contents"""
        for i, bucket in enumerate(self.table):
            print(f"Index {i}: {bucket}")

# Create a Simple Hash Table with n slots and without collision
simple_hash_table = HashTable(7)  # Hash table with 7 slots
# Insert the elements
simple_hash_table.insert(14, "land")
simple_hash_table.insert(22, "Banana")
simple_hash_table.insert(2, "Cherry")
simple_hash_table.insert(12, "Date")
simple_hash_table.insert(10, "Elderberry")
simple_hash_table.insert(11, "Guava")
simple_hash_table.insert(13, "Blueberry")

# Display the Simple hash table with no collission
print("\n Simple Hash Table Content:")
simple_hash_table.display()

# Create a Hash Table with n slots
hash_table = HashTable(7)  # Hash table with 7 slots
# Inserting values, some keys will collide if they have the same remainders
# on divsion by the size = 7
print("\nInsert the values in the hash table to create collision:")
hash_table.insert(14, "land")
hash_table.insert(21, "Banana")
hash_table.insert(2, "Cherry")
hash_table.insert(12, "Date")
hash_table.insert(9, "Elderberry")
hash_table.insert(11, "Guava")
hash_table.insert(8, "Blueberry")
# Try more values to full utlization of Hash Table of size 7
hash_table.insert(10, "Apple")
hash_table.insert(20, "Muskmellon")
hash_table.insert(30, "Orange")
hash_table.insert(17, "Rasberry")
# Display the hash table showing collisions
print("\nHash Table Content showing collision:")
hash_table.display()



____________________________________________________________________________Q1____________________________________________________________________________


# 1. Linear Probing
class LinearProbingHashTable:
    def __init__(self, size):
        self.size = size
        self.table = [None] * size  # Empty hash table

    def hash_function(self, key):
        return key % self.size  # Simple modulus hash function

    def insert(self, key, value):
        index = self.hash_function(key)
        original_index = index
        i = 0
        # Linear Probing: Find next available slot
        while self.table[index] is not None:
            print(f"Collision at index {index} for key {key}, trying next vacant slot...")
            i = i+1
            index = (original_index + i) % self.size  # important formula - Linear probing

        self.table[index] = (key, value)
        print(f"Inserted ({key}, {value}) at index {index}")

    def display(self):
        print("\nLinear Probing Hash Table:")
        for i, entry in enumerate(self.table):
            print(f"Index {i}: {entry}")
# Demonstration of Linear Probing
linear_hash_table = LinearProbingHashTable(7)
print("\n--- Linear Probing Demonstration ---")
linear_hash_table.insert(10, "Apple")  # 10 % 7 = 3
linear_hash_table.insert(20, "Banana") # 20 % 7 = 6
linear_hash_table.insert(30, "Cherry") # 30 % 7 = 2
linear_hash_table.insert(17, "Date")   # 17 % 7 = 3
print('Collision, resolved via linear probing')
print('and 17 is inserted at the vacant slot with index 4')
linear_hash_table.display()
print('\n\nCheck Linear Probing by adding 37 where 37 % 7 = 2, colliding with 30')
linear_hash_table.insert(37, "Guava")
print('Collision, resolved via linear probing')
print('and 37 is inserted at the vacant slot with index 5')
linear_hash_table.display()
print('\n\nAdd more elements say 48 to demonstarte how initial vacant slots are utlized')
linear_hash_table.insert(48, "Orange")
print('Collision, resolved via linear probing')
print('and 48 is inserted at the vacant slot with index 0')
linear_hash_table.display()
print('\n\nAdd more elements say 48 to demonstarte how initial vacant slots are utlized')
linear_hash_table.insert(19, "Watermellon")
print('Collision, resolved via linear probing')
print('and 19 is inserted at the vacant slot with index 1')
linear_hash_table.display()



_________________________________________________________________________________Q2________________________________________________________________________________

# 2. Quadratic Probing
class QuadraticProbingHashTable:
    def __init__(self, size):
        self.size = size
        self.table = [None] * size  # Empty hash table

    def hash_function(self, key):
        return key % self.size  # Simple modulus hash function

    def insert(self, key, value):
        print('Inserted key =',key)
        index = self.hash_function(key)
        original_index = index
        print('original_index of ',key,'=',original_index)

        i = 0 # i is re-intialized for collision resolution
        # Quadratic Probing: Find next available slot
        while self.table[index] is not None:
            print(f"Collision at index {index} for key {key}, trying next slot using quadratic probing...")
            i = i+1
            print('i =',i)
            print('i square =',i**2)
            index = (original_index + i**2) % self.size  # Quadratic probing
            print('index = original_index + i square =',index)
        self.table[index] = (key, value)
        print(f"Inserted ({key}, {value}) at vacant index {index}")

    def display(self):
        print("\nQuadratic Probing Hash Table:")
        for i, entry in enumerate(self.table):
            print(f"Index {i}: {entry}")

# Demonstration of Quadratic Probing
quadratic_hash_table = QuadraticProbingHashTable(7) # numbered from 0 to 6
print("\n--- Quadratic Probing Demonstration ---")
quadratic_hash_table.insert(10, "Apple")  # 10 % 7 = 3
quadratic_hash_table.insert(20, "Banana") # 20 % 7 = 6
quadratic_hash_table.insert(30, "Cherry") # 30 % 7 = 2
quadratic_hash_table.insert(17, "Date")   # 17 % 7 = 3
print('Collision, resolved via quadratic probing\n')
quadratic_hash_table.display()
print('Collision, resolved via quadratic probing\n')
quadratic_hash_table.insert(27, "Elderberry") # 27 % 7 = 6 (Collision, resolved via quadratic probing)
quadratic_hash_table.display()
print('Collision, resolved via quadratic probing\n')
quadratic_hash_table.insert(44, "Papaya")
# 44 % 7 = 2 (Collision, resolved via quadratic probing)
quadratic_hash_table.display()
print('Collision, resolved via quadratic probing\n')






class DoubleHashingHashTable:
    def __init__(self, size):
        self.size = size
        self.table = [None] * size  # Empty hash table
        self.prime = self.get_smaller_prime()
        # Prime number for secondary hashing will be received from the next functions
        print('self.prime =', self.prime)

    def get_smaller_prime(self):
        """Finds the largest prime smaller than table size for secondary hashing"""
        for num in range(self.size - 1, 1, -1):
          # range(start, stop, step)
            if self.is_prime(num):
                return num
        return 3  # Default to 3 if no prime found

    def is_prime(self, num):
        print('num =',num)
        """Check if a number is prime"""
        if num < 2:
            return False
        for i in range(2, int(num ** 0.5) + 1):
          # Using Sieve Principal - we need not check for the factors upto n, instead we can check upto n/2
            if num % i == 0:
                return False
        return True

    def primary_hash(self, key):
        """Primary hash function"""
        return key % self.size

    def secondary_hash(self, key):
        """Secondary hash function for step size"""
        return self.prime - (key % self.prime)

    def insert(self, key, value):
        """Insert a key-value pair using double hashing"""
        print('key =',key)
        index = self.primary_hash(key)
        print('index =',index)
        print('self.prime = ', self.prime)
        print('self.prime - (key % self.prime) =',self.prime - (key % self.prime))
        print('self.secondary_hash(key) = ', self.secondary_hash(key))
        step_size = self.secondary_hash(key)
        print('step_size =',step_size)
        original_index = index
        print('original_index =',original_index)
        i = 0

        # Double Hashing: Find next available slot
        while self.table[index] is not None:
            print(f"Collision at index {index} for key {key}, using double hashing...")
            i += 1
            print('i = ',i)
            index = (original_index + i * step_size) % self.size
            print('original_index =',original_index)
            print('step_size =',step_size)
            print('index =',index)
        self.table[index] = (key, value)
        print(f"Inserted ({key}, {value}) at index {index}")

    def display(self):
        """Display the hash table"""
        print("\nDouble Hashing Hash Table:")
        for i, entry in enumerate(self.table):
            print(f"Index {i}: {entry}")

# Demonstration of Double Hashing
double_hash_table = DoubleHashingHashTable(7)
print('self.size =',7)

print("\n--- Double Hashing Demonstration ---")
double_hash_table.insert(10, "Apple")  # 10 % 7 = 3
double_hash_table.insert(20, "Banana") # 20 % 7 = 6
double_hash_table.insert(30, "Cherry") # 30 % 7 = 2
double_hash_table.insert(17, "Date")   # 17 % 7 = 3 (Collision, resolved via double hashing)
double_hash_table.insert(27, "Elderberry") # 27 % 7 = 6 (Collision, resolved via double hashing)
double_hash_table.display()








___________________________________________________________________________________________________________________________________________________________________



class HashNode:
    """A node structure for linked list used in separate chaining"""
    def __init__(self, key, value):
        self.key = key
        self.value = value
        self.next = None  # Pointer to next node

class SeparateChainingHashTable:
    def __init__(self, size):
        self.size = size
        self.table = [None] * size  # Hash table with linked lists

    def hash_function(self, key):
        """Computes hash index"""
        return key % self.size

    def insert(self, key, value):
        """Inserts a key-value pair into the hash table"""
        index = self.hash_function(key)
        new_node = HashNode(key, value)

        if self.table[index] is None:
            self.table[index] = new_node  # Insert at empty index
        else:
            # Insert at the head of the linked list (for simplicity)
            current = self.table[index]
            while current:
                if current.key == key:
                    current.value = value  # Update value if key exists
                    return
                if current.next is None:
                    break
                current = current.next
            current.next = new_node  # Append new node at end
        print(f"Inserted ({key}, {value}) at index {index}")

    def search(self, key):
        """Searches for a key in the hash table"""
        index = self.hash_function(key)
        current = self.table[index]

        while current:
            if current.key == key:
                return current.value  # Key found
            current = current.next
        return None  # Key not found

    def delete(self, key):
        """Deletes a key from the hash table"""
        index = self.hash_function(key)
        current = self.table[index]
        prev = None

        while current:
            if current.key == key:
                if prev:
                    prev.next = current.next  # Remove from linked list
                else:
                    self.table[index] = current.next  # Remove first node
                print(f"Deleted key {key} from index {index}")
                return
            prev = current
            current = current.next
        print(f"Key {key} not found")

    def display(self):
        """Displays the hash table"""
        print("\nSeparate Chaining Hash Table:")
        for i, node in enumerate(self.table):
            print(f"Index {i}:", end=" ")
            current = node
            while current:
                print(f"({current.key}, {current.value}) ->", end=" ")
                current = current.next
            print("None")


# Demonstration of Separate Chaining
hash_table = SeparateChainingHashTable(5)  # Table size 5

print("\n--- Separate Chaining Demonstration ---")
hash_table.insert(10, "Apple")  # 10 % 5 = 0
hash_table.insert(20, "Banana") # 20 % 5 = 0 (Collision, separate chaining)
hash_table.insert(30, "Cherry") # 30 % 5 = 0 (Collision, separate chaining)
hash_table.insert(12, "Date")   # 12 % 5 = 2
hash_table.insert(7, "Elderberry") # 7 % 5 = 2 (Collision, separate chaining)

hash_table.display()

# Searching
print("\nSearching for key 12:", hash_table.search(12))
print("Searching for key 100:", hash_table.search(100))

# Deletion
hash_table.delete(20)
hash_table.delete(100)  # Non-existent key
hash_table.display()










# ALTERNATE_WAY_SEPERATE CHAINING
class Node:
    """A node in the linked list for separate chaining"""
    def __init__(self, key, value):
        self.key = key
        self.value = value
        self.next = None  # Pointer to the next node

class HashTable:
    """Hash Table using Separate Chaining"""
    def __init__(self, size):
        self.size = size
        self.table = [None] * size  # Array of linked lists

    def hash_function(self, key):
        """Hash function using modulo operation"""
        return key % self.size

    def insert(self, key, value):
        """Insert key-value pair into the hash table"""
        index = self.hash_function(key)
        new_node = Node(key, value)

        # If the bucket is empty, insert node
        if self.table[index] is None:
            self.table[index] = new_node
        else:
            # Insert at the beginning of the linked list (or traverse to the end)
            current = self.table[index]
            while current.next:
                if current.key == key:  # Update existing key
                    current.value = value
                    return
                current = current.next
            current.next = new_node
        print(f"Inserted ({key}, {value}) at index {index}")

    def search(self, key):
        """Search for a value by key"""
        index = self.hash_function(key)
        current = self.table[index]

        while current:
            if current.key == key:
                return current.value
            current = current.next
        return None

    def delete(self, key):
        """Delete a key-value pair from the hash table"""
        index = self.hash_function(key)
        current = self.table[index]
        prev = None

        while current:
            if current.key == key:
                if prev:
                    prev.next = current.next  # Remove node from linked list
                else:
                    self.table[index] = current.next  # Remove head node
                print(f"Deleted ({key}) from index {index}")
                return
            prev, current = current, current.next

        print(f"Key {key} not found!")

    def display(self):
        """Display the hash table"""
        print("\nSeparate Chaining Hash Table:")
        for i, node in enumerate(self.table):
            print(f"Index {i}:", end=" ")
            current = node
            while current:
                print(f"({current.key}, {current.value}) ->", end=" ")
                current = current.next
            print("None")

# Demonstration of Separate Chaining
hash_table = HashTable(7)

print("\n--- Separate Chaining Demonstration ---")
hash_table.insert(10, "Apple")  # 10 % 7 = 3
hash_table.insert(20, "Banana") # 20 % 7 = 6
hash_table.insert(30, "Cherry") # 30 % 7 = 2
hash_table.insert(17, "Date")   # 17 % 7 = 3 (Collision, linked list formed)
hash_table.insert(27, "Elderberry") # 27 % 7 = 6 (Collision, linked list formed)

hash_table.display()

# Searching
print("\nSearching for key 17:", hash_table.search(17))  # Expected output: Date
print("Searching for key 5:", hash_table.search(5))  # Expected output: None

# Deletion
hash_table.delete(17)
hash_table.display()

















___________________________________________________________________________________________________________________________________________________________________




class RehashingHashTable:
    def __init__(self, size):
        self.size = size
        self.count = 0  # Track the number of elements
        self.table = [None] * size
        self.load_factor_threshold = 0.7  # Rehash when load factor exceeds 0.7

    def hash_function(self, key):
        """Primary hash function"""
        return key % self.size

    def insert(self, key, value):
        """Insert key-value pair, with rehashing when necessary"""
        if self.count / self.size > self.load_factor_threshold:
            print("\nLoad factor exceeded! Rehashing table...")
            self.rehash()

        index = self.hash_function(key)
        original_index = index
        i = 0

        # Linear Probing for Collision Resolution
        while self.table[index] is not None:
            print(f"Collision at index {index} for key {key}, trying next slot...")
            i += 1
            index = (original_index + i) % self.size  # Linear probing

        self.table[index] = (key, value)
        self.count += 1
        print(f"Inserted ({key}, {value}) at index {index}")

    def rehash(self):
        """Rehash by doubling the table size and reinserting elements"""
        new_size = self.get_next_prime(self.size * 2)  # Get next prime number
        old_table = self.table
        self.size = new_size
        self.table = [None] * new_size
        self.count = 0  # Reset count

        # Reinsert elements into new table
        for item in old_table:
            if item is not None:
                self.insert(item[0], item[1])

    def get_next_prime(self, num):
        """Find the next prime number greater than the given number"""
        while True:
            if self.is_prime(num):
                return num
            num += 1

    def is_prime(self, num):
        """Check if a number is prime"""
        if num < 2:
            return False
        for i in range(2, int(num ** 0.5) + 1):
            if num % i == 0:
                return False
        return True

    def display(self):
        """Display the hash table"""
        print("\nRehashing Hash Table:")
        for i, entry in enumerate(self.table):
            print(f"Index {i}: {entry}")


# Demonstration of Rehashing
rehashing_hash_table = RehashingHashTable(5)  # Initial size 5

print("\n--- Rehashing Demonstration ---")
rehashing_hash_table.insert(10, "Apple")  # 10 % 5 = 0
rehashing_hash_table.insert(20, "Banana") # 20 % 5 = 0 (Collision)
rehashing_hash_table.insert(30, "Cherry") # 30 % 5 = 0 (Collision)
rehashing_hash_table.insert(25, "Date")   # 25 % 5 = 0 (Collision, triggers rehashing)
rehashing_hash_table.insert(15, "Elderberry") # New table size used

rehashing_hash_table.display()



















___________________________________________________________________________________________________________________________________________________________________


# Universal Hashing
import random

class UniversalHashing:
    def __init__(self, size, prime=101):  # Prime should be greater than table size
        self.size = size
        self.prime = prime
        self.a = random.randint(1, prime - 1)  # Random 'a' in range [1, p-1]
        self.b = random.randint(0, prime - 1)  # Random 'b' in range [0, p-1]
        self.table = [None] * size

    def hash_function(self, key):
        """Universal Hash Function"""
        return ((self.a * key + self.b) % self.prime) % self.size

    def insert(self, key, value):
        """Insert key-value pair into the hash table"""
        index = self.hash_function(key)
        while self.table[index] is not None:  # Handling collision (Linear Probing)
            index = (index + 1) % self.size
        self.table[index] = (key, value)
        print(f"Inserted ({key}, {value}) at index {index}")

    def display(self):
        """Display the hash table"""
        print("\nUniversal Hashing Table:")
        for i, entry in enumerate(self.table):
            print(f"Index {i}: {entry}")

# Demonstration
universal_hash_table = UniversalHashing(size=10)  # Hash table size 10

print("\n--- Universal Hashing Demonstration ---")
universal_hash_table.insert(10, "Apple")
universal_hash_table.insert(20, "Banana")
universal_hash_table.insert(30, "Cherry")
universal_hash_table.insert(17, "Date")
universal_hash_table.insert(25, "Elderberry")
universal_hash_table.display()

