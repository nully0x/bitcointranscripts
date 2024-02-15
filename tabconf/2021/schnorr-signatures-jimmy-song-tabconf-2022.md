---
title: "Schnorr Signatures - Jimmy Song - TABConf 2022"
transcript_by: nully0x via review.btctranscripts.com
media: https://www.youtube.com/watch?v=Ubp29_DJ5rM
speakers: ["Jimmy Song","Adam Ficsor","Adam Ludwin"]
categories: ["conference"]
date: 2021-11-10
---

## Intro

 Anyway, like I said, this is a technical talk and we're going to talk about Schnorr signatures and the benefits that it brings.
So let's get started.
So here's the agenda.
We're going to talk about, we're going to review the signature algorithm that's currently on Bitcoin.
This is Elliptic Curve Digital Signature Algorithm or ECDSA.
Then we're going to go describe what Schnorr signatures are.
And then we're going to go over all of the key and signature aggregation stuff that you can do or some of the benefits that you get out of Schnorr.
So let's get started.
Here is the Elliptic Curve Digital Signature Algorithm or ECDSA.
And we believe that Satoshi chose ECDSA back in 2009 because Schnorr was under patent.
Patent expired a couple of years later.
So we are able to use it now without any sort of like legal trouble or possibility thereof.
But it's actually, ECDSA is actually like a little more complicated than Schnorr as you'll see.
But anyway, the way it works is using some sort of like a private key, which we're going to call E.
Private key is a scalar.
It's a 256 bit number.
This is sort of like the secret that you have to keep away from other people.
The public key is the resulting point.
And if you are not familiar with Elliptic Curve cryptography or finite fields or elliptic curves, I do have a book, Programming Bitcoin, that describes a lot of it and goes through it like step by step.
So it's not going to make that much sense unless you know that stuff.
And that public key is actually two numbers.
It's a coordinate system.
An X coordinate and a Y coordinate.
And that's kind of important for what we're going to do.
All right.
So what does ECDSA actually look like?
Here's the actual overview of it.
The main equation in ECDSA is this.
Z over SG plus R over SP equals R comma Y.
And it's a little bit like, if you haven't seen this before, it's kind of confusing because people don't know what these things stand for.
But the thing in front of the capital letters is a scalar of some kind.
It's a 256 bit number.
And the division that's being done is what you would call group division or field division.
It's not the division that you think.
And it's actually quite costly on the CPU.
All right.
But R is the result committed by R divided by S times P.
So you're committing to the result that you're going to get.
So you evaluate the left side of the equation and you're expecting little r to come up.
But that little r also shows up right before P.
So you commit to the target that you're going to hit.
You're committing to the result that you're going to get by putting it into that equation.
Z is the hash of the message.
So in Bitcoin, this can be any message that you want.
But generally, it's a transaction that you are performing.
So it's generally on a per input basis.
A, like, I want this transaction to go through.
So I am committing to this particular message.
And I am signing this particular message.
And that's Z divided by S times G.
And S is computed by the signer.
So this is where the division stuff comes in.
Which requires the private key E.
So S cannot be computed without the secret, the private key.
And that's the key to how signing works.
But that's a general overview.
The actual verification algorithm, once again, uses this equation.
## VERIFICATION ALGORITHM

 And basically, we already know the hash of the message or what message was signed.
We already know the public key that's been communicated to us in Bitcoin.
That's obvious because it's in the script sig or in the witness field.
And we also have the signature.
And the signature is a pair, R comma S.
R is the committed target, right, where we're going with this equation.
And S is the thing that makes all of the variables work.
And the verifier calculates the left side of that equation, Z divided by S times G plus R divided by S times P.
And sees if the result is the value that it was committed to.
And the commitment is only for the x-coordinate.
It's R.
That's it.
And if that R matches the R that you used in the left side of the equation, then you know that the signer actually knew the secret.
That's the key to what ECDSA is.
The signature algorithm is very much standard.
Z is the hash of the message.
You start with that.
You know the public key.
You know the secret.
You generate a nonce, a K.
And this nonce stands for number used only once.
You're only supposed to use it once.
And you compute KG, which has that R-coordinate.
And you're going to use that R-coordinate along with your secret and the Z and the K to get this number S.
And that is essentially your signature, R and S.
And it turns out everything goes through because of this equation, Z divided by S times G plus R divided by S times P.
We know that P is E times G.
So we can factor that out in the second part.
Z over S times G plus RE over S times G.
And then you can combine the terms because it's a scalar on front.
And you get Z plus RE divided by S.
And if you look at the definition of S, two lines above, you get S equals Z plus RE divided by K.
And you sub that.
And you get KG.
KG, as before, was R comma Y.
So everything sort of just goes through.
And you can prove that the target that you committed to is, the result that you committed to, is actually the result that actually happens.
And that's how you sign something so that a verifier can know that you actually hold the secret.
That's how ECDSA works.
This seems a little backwards.
It's because it kind of is.
Because Schnorr was created first before ECDSA.
And there are lots of signature and verification algorithms.
But in order to sort of get around the Schnorr patent, this is what Satoshi kind of had to use.
But the big thing to notice about ECDSA is that both signing and verification rely on some sort of field division or group division or whatever you want to call it.
It's division.
And that is a very intensive computer for any sort of processor.
If you study this stuff, the cycles that division uses is a lot higher than almost any other operation.
And this is because we're doing finite field math.
Again, you can read my book, Programming Bitcoin.
It'll describe exactly why.
But basically, it's a very large exponent that you have to take it to.
The signer commits to just the x-coordinate r.
So that means that it doesn't commit to the entire point.
So you can't do certain things that would be nice.
If it committed to the entire point, then we could do things like batch verification and signature aggregation, which Schnorr allows.
But because ECDSA only commits to the x-coordinate, you can't add or subtract or anything like that.
Because a lot of optimizations have been made on Bitcoin based on this property that you only need to commit to the x-coordinate.
And the y-coordinate can be whatever.
And if the x is valid, then there are two possible y's every time.
So it makes it a little bit harder.
The commitments to r and s are separate, right?
Like r divided by s times g, so that it's in a separate term.
Then r divided by s times p.
And the z is z divided by s times g.
So they're in separate terms because you have to commit to them separately.
There are all sorts of weird attacks that you can do if you commit to them at the same time.
So those are some of the weaknesses of ECDSA.
All right, so here's what a Schnorr signature is like.
It relies on a cryptographically secure hash function, H, instead of division.
And that's the key.
We can use this additional construct called a hashing function, a cryptographically secure hashing function, which has pre-image resistance, and collision resistance.
And collision resistance, it's very difficult to find a hash that goes to a certain value.
And the signer can commit to multiple things at once, just by hashing them together, right?
Like you can hash multiple things and serialize them and add them together or whatever.
And that commits you to those values because you can't find the hash pre-image.
That's the key.
So here's an overview of how that works.
## OVERVIEW

 This is the key equation, much like in ECDSA.
It's SG minus the hash of RP and Z times P equals R.
And R is the result that's actually committed, right?
Like you notice that R is on both sides of the equation.
R is the result that we're going to get, but it's also committed beforehand through that hash.
Z is the hash of the message, and it's also committed in that hash.
You can kind of do it at once.
And in fact, you can see there that it's not just committing to the result and the hash of the message, but we're also committing to the public key.
That's actually, so that you don't do anything weird with it.
And S is computed by the signer, which requires the private key E.
So this is very similar to ECDSA in that regard.
You have E, which is used to compute S.
So here's what the verification algorithm looks like.
SG minus the hash of RP and Z times P equals R.
That's the equation.
Z is the hash of the message, which this verifier knows.
P is the public key, which the verifier knows.
The signature is the pair capital R, S, which the verifier knows.
Okay, that's enough to actually run this equation.
And the verifier calculates to see if the equation on the left side, SG minus hash of RP and Z times P equals R.
And if it does actually go to R, then they know that whoever signed it knows the secret.
That's the key.
That's what all verification algorithms essentially do.
The actual signature algorithm is very similar to ECDSA in that the Z is the hash of the message.
We know the secret E, which has the public point P.
You generate a nonce, and you can go look up bit 340.
It has a very specific way to generate the nonce.
But you generate some sort of nonce, a number used only once.
And you compute the resulting point from K, and you get R.
And you compute S based on this formula, K plus the hash of the committed result, the committed pub key, the committed hash of the message, times the secret.
And that definitely requires the private key.
The signature, again, is the pair, the resulting point, and S.
And you can see that everything kind of canceled.
SG minus H of RPZ times P.
And we know that P is E times G, so we can sort of collect the terms together.
We also know what S is.
And you collect all the terms together, H of RP and Z times E cancel each other out.
So you get KG, and KG is defined as R.
So you get what you would expect, and that's how the signature algorithm in Schnorr works.
So the key thing here is that both the signing and verification rely on that cryptographically secure hash function H instead of division, right?
Like in ECDSA, you need a very expensive operation in order to do it.
This just requires a hashing function, which is a lot less expensive for a CPU.
And the signer commits to a resulting point, R, instead of just the X coordinate.
And this is what gives us sort of like the magical properties that we're gonna sort of like look at shortly.
But it's not just the X coordinate, it's the entire point, right, R.
And that's huge, because, and also the commitments to R and Z are combined in a single hash instead of having different terms for it.
With ECDSA, you had Z over S and then R over S.
So different terms have different commitments.
This one, it's just in a single hash.
You could commit to all sorts of things in that hash.
All right, so we can commit to even more stuff, like the public key that we're using.
So what does this all mean?
That means that we get certain advantages with Schnorr.
We get certain abilities that we didn't have before, because the result is a point.
We commit to a point, right?
And that means we can do batch verification.
We can do signature aggregation, and we can do pub key aggregation.
So let's start with batch verification.
## BATCH VERIFICATION

 So the equation I gave you before is SG minus hash of R, P, and Z times P, the public point P equals R.
That was it.
And you can have lots and lots of those.
For a transaction with 30 inputs, you would have 30 of these.
Or for a block with thousands of inputs, you can have thousands of these.
The key is that because the right side is a point and you're not committing just to the x coordinate, this equation works.
You can sum over all of the different eyes, all of the different inputs in a particular transaction, or all of the inputs in a particular block, or even all of the inputs in the entire blockchain, right?
Like as long as everything's in Schnorr, you can verify them all at once.
And you can check this, and you can move some of the terms around, and you can get this equation at the end.
And the key to the efficiency of this particular equation is that the left side is just modulo arithmetic.
And you just add up all the little s's.
And the right side is a little more expensive, but you get a bunch of point addition in the last term here.
The sum from i to n of r sub i, which is not that expensive.
And then you have point multiplication with an arbitrary point in the middle.
Those are the most expensive, but you get them all out of the way at once.
So you get a lot more efficiency with batch verification.
You can verify 40 transactions at once, right?
If they only use Schnorr signatures, then you can do this, because you are committing to a point and not an x coordinate.
That's the key, and that's one of the properties that we get out of Schnorr.
The actual batch verification, by the way, is a little more complicated.
And there are certain attacks that it protects against.
So there are all these coefficients in front of r and stuff like that.
You can go look up the recommended way, and I believe in bit 340.
So you can go look that up.
But that's the basic idea.
The other thing that we can do is we can do something called signature aggregation.
And this is the ability to produce a single signature, RS, by a group of public keys.
You can have lots of public keys, 1 through n, and they can produce a single signature that's essentially signed by all of them.
So this is n of n, right?
And each public key has a private key, and that's how we denote it, e sub i and p sub i.
And L is sort of like a commitment to this group of public keys.
And we can use the same or different hash function.
And every single one of those private key holders creates their own nonce, K sub i, and you get the resulting point, R sub i.
And capital R, the commitment, committed point that we're going to, is going to be the sum of all those points.
And finally, C sub i is this hash commitment to L, which is a commitment to every single one of those pub keys.
And this particular pub key, along with R and Z, which we know is needed as part of the signature algorithm.
And the actual S that makes everything work is K sub i plus C sub i, E sub i, and the little s ends up being the sum of all of the S sub i's.
And it turns out that if you do this, S sub, SG minus C sub i, P sub i.
You can, we know what P sub i is.
It's E sub i times G, and we can combine the terms there.
And S i minus C sub i, E sub i, if you substitute K sub i plus C sub i, E sub i, that ends up canceling out.
So you just get K sub i, G, which is R sub i.
And the sum of the R sub i's is R as it is like three lines above.
So you end up getting the result that you want.
And that's what we call signature aggregation of various signatures.
So you get a signature from each member of this pub key group.
And you're able to combine them and have a single signature that represents all of them, which is kind of remarkable.
And this was, I think, Bellara and Navin, and that's the paper that it comes from.
But you can actually do better.
Whoops.
What you can do is you can go to pub key aggregation.
## PUBLIC KEY AGGREGATION

