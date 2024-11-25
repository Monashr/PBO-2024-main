# Java Inner Classes

Berikut beberapa keuntungan menggunakan inner class:

- Membuat kode menjadi bersih dan mudah dibaca.
- Metode privat dari outer class dapat diakses, sehingga membawa dimensi baru dan membuatnya lebih dekat dengan dunia nyata.
- Optimisasi kode.

## Perbedaan Subclass dan Innerclass

Dalam Java, subclass dan inner class adalah dua konsep yang berbeda meskipun keduanya digunakan untuk mendefinisikan kelas di dalam konteks tertentu.

### Subclass

Subclass adalah sebuah kelas yang mewarisi properti dan metode dari kelas lain (disebut superclass). Konsep ini berkaitan dengan pewarisan (inheritance) dalam paradigma OOP (Object-Oriented Programming), yang memungkinkan subclass untuk mengambil semua sifat dari superclass dan menambah atau mengubahnya sesuai kebutuhan.

Subclass digunakan untuk memperluas fungsionalitas kelas yang sudah ada tanpa mengubah kode asli dari superclass. Subclass dapat mengakses anggota publik dan protektif dari superclass, dan dapat menimpa (override) metode superclass.

Subclass dibuat menggunakan kata kunci extends untuk mewarisi kelas lain.

```java
class Animal {
    void speak() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    void speak() {
        System.out.println("Dog barks");
    }
}
```

### Inner Class

Inner class adalah kelas yang dideklarasikan di dalam kelas lain. Inner class bisa mengakses anggota kelas luar (outer class) bahkan yang bersifat privat. Inner class dapat digunakan untuk mengorganisir kode yang lebih terstruktur atau untuk menciptakan hubungan yang lebih dekat antara kelas luar dan kelas dalam.

```java
class OuterClass {
    private String outerField = "Outer Field";

    class InnerClass {
        void printOuterField() {
            System.out.println(outerField); // Mengakses anggota outer class
        }
    }
}
```

## Jenis-jenis Inner Class

Pada Java terdapat empat jenis inner class sebagai berikut:

1. Inner Class Regular
   Inner class yang didefinisikan secara langsung di dalam sebuah kelas.

2. Static Nested Class
   Inner class yang bersifat static sehingga tidak bergantung pada objek dari kelas luar.

3. Local Inner Class
   Inner class yang didefinisikan di dalam sebuah metode.

4. Anonymous Inner Class
   Inner class tanpa nama, biasanya digunakan untuk membuat implementasi instan dari interface atau kelas abstrak.

### Java Regular Inner Classes

Dalam Java, juga memungkinkan untuk membuat kelas di dalam kelas (nested class). Tujuan dari nested class adalah untuk mengelompokkan kelas-kelas yang saling berkaitan, sehingga membuat kode Anda lebih mudah dibaca dan dipelihara.

Untuk mengakses inner class, buatlah objek dari kelas luar terlebih dahulu, kemudian buat objek dari inner class:

```java
class OuterClass {
  int x = 10;

  class InnerClass {
    int y = 5;
  }
}

public class Main {
  public static void main(String[] args) {
    OuterClass myOuter = new OuterClass();
    OuterClass.InnerClass myInner = myOuter.new InnerClass();
    System.out.println(myInner.y + myOuter.x);
  }
}

// Outputs 15 (5 + 10)
```

### Regular Private Inner Class

Berbeda dengan kelas "biasa", sebuah inner class dapat memiliki modifier akses seperti private atau protected. Jika Anda tidak ingin objek lain di luar kelas mengakses inner class, Anda bisa mendeklarasikan kelas tersebut sebagai private.

Dengan cara ini, inner class hanya bisa diakses di dalam kelas tempat kelas tersebut didefinisikan, sehingga membatasi aksesnya dari luar. Ini membantu menjaga enkapsulasi dan membatasi penggunaan kelas tersebut hanya untuk kebutuhan internal.

```java
class OuterClass {
  int x = 10;

  private class InnerClass {
    int y = 5;
  }
}

public class Main {
  public static void main(String[] args) {
    OuterClass myOuter = new OuterClass();
    OuterClass.InnerClass myInner = myOuter.new InnerClass();
    System.out.println(myInner.y + myOuter.x);
  }
}
```

Jika Anda mencoba mengakses inner class yang bersifat private dari kelas luar, maka akan terjadi error:

```bash
Main.java:13: error: OuterClass.InnerClass has private access in OuterClass
    OuterClass.InnerClass myInner = myOuter.new InnerClass();
              ^
```

### Static Inner Class

Sebuah inner class juga dapat bersifat static, yang berarti Anda dapat mengaksesnya tanpa perlu membuat objek dari kelas luar.

```java
class OuterClass {
  int x = 10;

  static class InnerClass {
    int y = 5;
  }
}

public class Main {
  public static void main(String[] args) {
    OuterClass.InnerClass myInner = new OuterClass.InnerClass();
    System.out.println(myInner.y);
  }
}

// Outputs 5
```

### Local Inner Class

Local Inner Class adalah kelas yang dideklarasikan di dalam metode atau blok kode suatu kelas luar. Class ini hanya dapat diakses dan digunakan dalam metode atau blok tersebut. Kelas ini memungkinkan pengelompokan kode yang relevan secara lokal di dalam metode tertentu, sehingga menjaga enkapsulasi dan keterbacaan.

Local Inner Class dapat mengakses variabel lokal dan parameter dari metode tempat ia dideklarasikan, namun variabel tersebut harus bersifat final. Kelebihan penggunaan Local Inner Class adalah membantu menyederhanakan kode dengan mendeklarasikan kelas yang hanya dibutuhkan dalam konteks tertentu, tanpa perlu mendeklarasikan kelas tersebut di luar metode.

```java
class OuterClass {
    void display() {
        class LocalInnerClass {
            void show() {
                System.out.println("Hello from Local Inner Class!");
            }
        }

        LocalInnerClass local = new LocalInnerClass();
        local.show();
    }

    public static void main(String[] args) {
        OuterClass outer = new OuterClass();
        outer.display();
    }
}
```

### Anonymous Inner Class

Anonymous Inner Class adalah kelas yang tidak memiliki nama dan biasanya didefinisikan serta digunakan langsung dalam ekspresi. Kelas ini sering digunakan untuk implementasi interface atau subclassing kelas yang hanya digunakan sekali, sehingga mengurangi kebutuhan untuk membuat kelas terpisah.

Anonymous inner class dibuat dengan cara mendeklarasikan kelas baru langsung di tempat instansiasi objek, dan sering kali digunakan untuk menyediakan implementasi metode secara langsung, seperti dalam event handling atau threading. Keuntungannya adalah menyederhanakan kode dengan menghindari pembuatan kelas terpisah, meskipun keterbatasannya adalah sulitnya untuk mengelola dan memperluasnya.

```java
abstract class Greeting {
    abstract void sayHello();
}

public class OuterClass {
    public static void main(String[] args) {
        Greeting greeting = new Greeting() {
            @Override
            void sayHello() {
                System.out.println("Hello from Anonymous Inner Class!");
            }
        };

        greeting.sayHello();
    }
}
```
