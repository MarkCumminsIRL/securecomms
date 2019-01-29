# Lab 2B: Classic Ciphers and the command line

In this lab we will learn some basic linux bash commands. We will re-use some of our earlier lab on classic ciphers, but this time we will attempt to script the solution to each of the problems rather than using online tools.

___

## Lab Contents

1. Introducing the translate(tr) command.
    + Some additional options for the tr command.
2. Rotational ciphers on the command line.
3. Using the alias Command.
4. Adding commands to the ~/.bashrc file.
5. Using functions to check all encodings.
6. Lab Summary / Cheat-Sheet.

___

### Introducing the translate(tr) command

The tr command in UNIX/Linux is a command line utility for translating or deleting characters. It supports a range of transformations including uppercase to lowercase, squeezing repeating characters, deleting specific characters and basic find and replace. It can be used with pipes to support more complex translation.

OK, so how does it work?

Syntax :

```bash
tr [OPTION] SET1 [SET2]
```

Basically we can use tr to translate SET1 to SET2, so we could use something like [a-z] and [A-Z] as SET1 and SET2, which would translate any lowercase letters into uppercase letters.

Example :

```bash
$ Echo 'lower case letters' | tr [a-z] [A-Z]
LOWER CASE LETTERS
```

> We can also use some special keywords such as: :lower:, :upper:, :digit: for a full list of available keywords you should look at the man page for the tr command.

#### Some additional options for the tr command

If we just pass SET1 and SET2 into to the tr command it will just convert any characters in SET1 into the equivalent character in SET2. However there are some additional options we can also use.

Options
>-c : complements the set of characters in string.i.e., operations apply to characters not in the given set\
>-d : delete characters in the first set from the output.\
>-s : Squeeze - replaces repeated characters listed in the set1 with single occurrence\
>-t : truncates set1

Lets have a quick look at some examples of each to better understand what is going on.

If we wanted to remove maybe all the digits from some file or string, we could use

```bash
$ echo "Welcome To 123 Secure Communications 101" | tr -d [:digit:]
Welcome To Secure Communications
```

If we wanted the opposite result from the last example, say we want just the digits and wanted to delete the characters we could just delete the :alpha: characters or we could get the compliment (or inverse) of our last result. For example, to remove all characters except digits, you can use the following.

```bash
$ echo "Welcome To 123 Secure Communications 101" | tr -cd [:digit:]
123101
```

If we wanted to squeeze any repeated spaces from our string we could use the following example.

```bash
$ echo "Welcome    To    Secure     Communications" | tr -s [:space:] ' '
Welcome To Secure Communications
```

> -t  may  be  used only when translating.  SET2 is extended to length of SET1 by repeating its last character as necessary.
> Excess  characters of  SET2  are  ignored.

### Rotational ciphers on the command line

So now that we have seen a bit of what can be done with the tr command lets try use it to solve some simple ciphers for us. We will start with the simple rot5 cipher.

rot5 is similar to the classic rot13 cipher used to rotate all 25 alpha characters, except rot5 is used to rotate through all 10 digits. So each digit is rotated 5 shifts. And like rot13 over alpha characters we can use rot5 to encrypt and decrypt.

So for this example lets create a file digits.txt that we will try to encrypt and then decrypt using tr to implement rot5.

First create our file

```bash
echo "Our digits are: 56789" > digits.txt
```

So if we wanted to use tr to implement to rot5 cipher we could use the following code snippet:

```bash
$cat digits.txt | tr [0-9] [5-90-4]
Our digits are: 01234
```

OK, can you follow the same logic and create a rot13 cipher using the tr command? We will try to decrypt the example given from our earlier classic ciphers lab. So try decode the following rot13 encoded string.

> EBG 13 JNF HFRQ OL ZVPEBFBSG SBE RAPBQVAT JVAQBJF ERTVFGELRAGEVRF

Hopefully you managed to figure out how to decode the previous example. So lets continue and try decode some of the other examples again from our earlier lab. So try decode the following examples using the tr command.

> HINT: You can combine multiple cases to the translate function to handle both upper and lower case letter at the same time. Try using sets similar to the following [a-z][A-Z] etc.

Decode this classic Caesar’s cipher:
> Wkh ruljlqdo Fdhvdu flskhu dozdBv xvhg d vkliw ri wkuhh

See if you can figure out how you might decode this rot47 encoded string?
>(:E9 6IA6C:6?46 J@F H:== DE2CE E@ C64@8?:D6 E96 492C24E6C D6ED @7 6249 6?4@5:?8]

### Using the alias Command

Hopefully by now you realise the power of the simple tr command. Wouldn't it be nice if we could somehow store some of the more useful variations that we might use again and again like rot13 or caesar etc. Well by using the alias command we can do just that, allowing us to create a shortcut to our commands so we don't have to retype them. So let us see how it works by creating a simple rot5 alias and see how we might use it. Try the following:

```bash
$ alias rot5='tr [0-9] [5-90-4]'
$ echo '12345' | rot5
67890
```

We can even use our new alias command to encrypt then decrypt a simple string like in this example. Which passed the original string to rot5 then passes the resulting encoded string into rot5 again which decodes it. You should try doing the same with a rot13 script to verify it encodes then decodes correctly.

```bash
$ echo '12345' | rot5 | rot5
12345
```

Using the alias command can be extremely useful for creating your own shortcuts for any commands, so always have it in the back of your mind if you have commands you use all the time.

### Adding commands to the ~/.bashrc file

One issue with the example we've shown so far is that when we close our current terminal window any alias we've created will be lost forever. So most likely you will probably want to keep some of your aliases permanently. To achieve this we need to add our aliases to our bashrc file. So todo this we need to edit our bashrc file in whatever text edit you wish and then add out alias to this file. This file will be loaded every time we start a new bash shell, and we will have all our aliases ready and waiting for us.

So open the file in nano or whatever editor you prefer

```bash
nano ~/.bashrc
```

And then add your alias command near the bottom of the file, you'll probably see some other aliases already included in your bashrc file.

When you are done, exit your bashrc file (control x). You'll also need to force your terminal to reload the bashrc file so your new aliases take effect. we can do this by typing the following in our terminal.

> Note the leading . (dot)

```bash
. ~/.bashrc
```

Create some aliases for yourself for rot5, rot13, rot47, caesar_enc, caesar_dec

### Lab Summary / Cheat-Sheet
