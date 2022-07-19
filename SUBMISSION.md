# Part A

## Part A.1

TODO:

## Part A.2

TODO:

# Part B

## Part B.1

The problem with the BattleRoyaleNumbers circuits is that they are missing a public input signal that refers to some commitment that a user has made somewhere. Because of this, users can always choose a number that is different from their original secret number in order to generate a validity proof, without anyone else knowing that they have chosen a different number, which is against the rules of the game.

Here is an example attack:

1. User1 selects secret number as 141472001
2. User2 selects secret number as 10000000000000000000000000000
3. Round 1 is a LessThan challenge against public number 999999945645649991
4. User1 generates validity proof using original secret number 141472001.
5. User2 generates validity proof using number secret number 141472001.

## Part B.2

The problem with the PickACard circuit is that it is vulnerable to brute-force attacks due to the incredibly small search space (52, precisely) for a hash that is the same as that of a player's secretly chosen card. In other words, since the private input `commitedCard` can only be within the range `0-51`, there can only be 52 possible `hashCommitment` values that are output, and a brute-force attack would involve the attacker only needing to pre-compute the values of these 52 `hashCommitment` values for them to be able to match against what each player secretly chose.

## Part B.3

The problem with the WorldNumbers circuit is that the signal `expectedHash` is a private signal, which makes it impossible for the smart contract verifier to check whether the `expectedHash` value is equal to the one that is already committed on-chain. With this circuit, a user can always generate a valid proof using any `mySecretLocation` and `expectedHash` combination - they don't need to be the same as the one that is committed on-chain.

## Part B.4

The problem with the OneOfMyCards circuits is that the `booleanUseCard1` and `booleanUseCard2` inputs are not restricted to being either 0 or 1. This means that, both cards can be used - even more than once - to pass the sum check at the end of the circuit. Here is an example of an attack:

1. User1 decides `card1` chosen as 1, `card2` chosen as 2, both hashes committed on-chain.
2. Given `requiredCard` is 5, User1 can generate a valid proof by using 1 and 2 for the `booleanUseCard1` and `booleanUseCard2` private inputs respectively.
