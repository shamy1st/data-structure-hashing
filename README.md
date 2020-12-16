# Hashing

![](https://github.com/shamy1st/data-structure/blob/main/images/hashtable.png)

--  | put | remove | get | containsKey | containsValue
----|-----|--------|-----|-------------|--------------
Map | O(1)| O(1)   | O(1)| O(1)        | O(n)

* **Interview Problems**
  * **First Non-Repeated Character**

          public class Main {
              public static void main(String[] args) {
                  System.out.println(findFirstNonRepeatedChar("a green apple")); //g
              }

              public static Character findFirstNonRepeatedChar(String str) {
                  Map<Character, Integer> map = new HashMap<>();

                  for(char ch : str.toCharArray()) {
                      int count = map.containsKey(ch) ? map.get(ch) : 0;
                      map.put(ch, count+1);
                  }

                  for(char ch : str.toCharArray()) {
                      if(map.get(ch) == 1)
                          return ch;
                  }
                  return null;
              }
          }

  * **First Repeated Character**

          public class Main {
              public static void main(String[] args) {
                  System.out.println(findFirstRepeatedChar("a green apple")); //e
              }

              public static Character findFirstRepeatedChar(String str) {
                  Set<Character> set = new HashSet<>();

                  for(char ch : str.toCharArray()) {
                      if(set.contains(ch))
                          return ch;
                      set.add(ch);
                  }
                  return null;
              }
          }

* **Collisions**
![](https://github.com/shamy1st/data-structure/blob/main/images/collisions.png)

  * **Chaining**
  ![](https://github.com/shamy1st/data-structure/blob/main/images/chaining.png)
  
        public class Main {
            public static void main(String[] args) {
                HashTable hashtable = new HashTable(5);
                hashtable.put(1, "A");
                hashtable.put(2, "B");
                hashtable.put(3, "C");
                hashtable.put(4, "D");
                hashtable.put(5, "E");
                hashtable.put(6, "F");
                hashtable.put(1, "Z");

                System.out.println(hashtable.get(4));
                System.out.println(hashtable.get(8));

                hashtable.remove(4);
                //hashtable.remove(9);

                hashtable.print();
            }
        }

        public class HashTable<K, V> {
            private class Entry<K, V> {
                private K key;
                private V value;

                public Entry(K key, V value) {
                    this.key = key;
                    this.value = value;
                }

                @Override
                public String toString() {
                    return "Entry{" + key + ", " + value + "}";
                }
            }

            private LinkedList<Entry<K, V>>[] items;

            public HashTable(int capacity) {
                items = new LinkedList[capacity];
            }

            public void put(K key, V value) {
                int bucketIndex = hash(key);
                if(items[bucketIndex] == null)
                    items[bucketIndex] = new LinkedList<>();

                for(var entry : items[bucketIndex]) {
                    if(entry.key == key) {
                        entry.value = value;
                        return;
                    }
                }
                items[bucketIndex].add(new Entry(key, value));
            }

            public V get(K key) {
                int bucketIndex = hash(key);
                if(items[bucketIndex] == null)
                    return null;

                for(var entry : items[bucketIndex]) {
                    if(entry.key == key) {
                        return entry.value;
                    }
                }
                return null;
            }

            public void remove(K key) {
                int bucketIndex = hash(key);
                if(items[bucketIndex] == null)
                    throw new IllegalStateException();

                for(var entry : items[bucketIndex]) {
                    if(entry.key == key) {
                        items[bucketIndex].remove(entry);
                        return;
                    }
                }
                throw new IllegalStateException();
            }

            private int hash(K key) {
                return key.hashCode() % items.length;
            }

            public void print() {
                for(int i=0;i<items.length;i++) {
                    if(items[i] != null) {
                        System.out.println(i + " : " + items[i].toString());
                    } else {
                        System.out.println(i + " : " + null);
                    }
                }
            }
        }
  
  * **Open Addressing**
  ![](https://github.com/shamy1st/data-structure/blob/main/images/probing.png)
  
    * **Linear Probing**
    ![](https://github.com/shamy1st/data-structure/blob/main/images/linear-probing.png)
    
    * **Quadratic Probing**
    ![](https://github.com/shamy1st/data-structure/blob/main/images/quadratic-probing.png)
    ![](https://github.com/shamy1st/data-structure/blob/main/images/quadratic-probing-2.png)
    
    * **Double Hashing**
    ![](https://github.com/shamy1st/data-structure/blob/main/images/double-hashing.png)
    ![](https://github.com/shamy1st/data-structure/blob/main/images/double-hashing-2.png)
