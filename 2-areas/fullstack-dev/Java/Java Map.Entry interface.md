---
created: 2024-08-13T09:03
updated: 2024-08-13T09:05
---
| Method                                                                                          | Description                                                                                                                          |
|-------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| K getKey()                                                                                      | It is used to obtain a key.                                                                                                          |
| V getValue()                                                                                    | It is used to obtain value.                                                                                                          |
| int hashCode()                                                                                  | It is used to obtain hashCode.                                                                                                       |
| V setValue(V value)                                                                             | It is used to replace the value corresponding to this entry with the specified value.                                                |
| boolean equals(Object o)                                                                        | It is used to compare the specified object with the other existing objects.                                                          |
| static <K extends Comparable<? super K>,V> Comparator<Map.Entry<K,V>> comparingByKey()          | It returns a comparator that compare the objects in natural order on key.                                                            |
| static <K,V> Comparator<Map.Entry<K,V>> comparingByKey(Comparator<? super K> cmp)               | It returns a comparator that compare the objects by key using the given Comparator.                                                  |
| static <K,V extends Comparable<? super V>> Comparator<Map.Entry<K,V>> comparingByValue()        | It returns a comparator that compare the objects in natural order on value.                                                          |
| static <K,V> Comparator<Map.Entry<K,V>> comparingByValue(Comparator<? super V> cmp)             | It returns a comparator that compare the objects by value using the given Comparator.                                                |


[[java]] [[Java Map Interface]] [[Map Methods]]