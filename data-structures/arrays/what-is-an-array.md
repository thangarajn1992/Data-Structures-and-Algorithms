# What is an Array?

> An Array is a collection of items. The items could be integers, strings, DVDs, games, books—anything really. The items are stored in neighboring \(contiguous\) memory locations. Because they're stored together, checking through the entire collection of items is straightforward.

So, how can we relate this back to the physical DVDs? Well, do you keep your DVDs all around the house in multiple locations? Hopefully not! Most people keep all of their DVDs right next to one another inside one gigantic box, or perhaps on a bookshelf. We do this so that if we need to find a particular DVD, we can quickly search through all of them without running from room to room.

#### Creating an Array <a id="creating-an-array"></a>

On a computer, Arrays can hold up to `N` items. The value of `N` is decided by you, the programmer, at the time you create the Array. This is the same as when we found a big enough cardboard box for the DVDs. Additionally, you also need to specify the _type_ of item that will be going into the Array.

In **Java**, we use the following code to create an Array to hold up to 15 DVDs. Note that we've also included a simple definition of a DVD for clarity.

```java
// The actual code for creating an Array to hold DVD's.
DVD[] dvdCollection = new DVD[15];

// A simple definition for a DVD.
public class DVD {
    public String name;
    public int releaseYear;
    public String director;

    public DVD(String name, int releaseYear, String director) {
        this.name = name;
        this.releaseYear = releaseYear;
        this.director = director;
    }

    public String toString() {
        System.out.println(
            this.name + ", directed by " + this.director + ", released in " + this.releaseYear));
    }
}
```

After running the above code, we now have an Array called `dvdCollection`, with `15` places in it. Each place can hold _one_ DVD. At the start, there are _no_ DVD's in the Array; we'll have to actually put them in.

The Array can only hold up to `15` DVDs. If we get a 16th DVD, we'll need to make a new Array. We'll look at how we deal with running out of space, in the next chapter.

Before we move onto actually putting some DVDs into the Array, though, one thing you might be wondering is why we'd make an Array with _only_ `15` places. Why not just make it hold `1000000` DVDs so that we _know for sure_ we'll always have enough space?

Well, the reason is the same as it is for the physical box of DVDs. Do you really want to find a box that could hold `1000000` DVDs when you currently only have `15` DVDs and, in fact, never expect to own more than `100` of them? Is it even worth getting a box that could hold `100` DVDs right now, when you only expect to get a few new ones each year? It will take up a lot more space in your home in the meantime.

It's exactly the same with the Array, where the space in your home is analogous to memory on the computer. If you make an Array with `1000000` spaces, the computer will reserve memory to hold `1000000` DVDs, even if you only put `15` DVDs into it. That memory can't be used for anything else in the meantime—just like the space in your house that has been taken over by that _huge_ cardboard box!

