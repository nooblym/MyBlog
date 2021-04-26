# SM-2

> SM-2是间隔重复算法的一种

## 算法描述

- **repetitions** - this is the number of times a user sees a flashcard. `0` means they haven't studied it yet, `1` means it is their first time, and so on. It is also referred to as `n` in some of the documentation.

  此参数表示用户看到的数量，0表示用户还没见过，1表示见过一次，以此类推，在一些文档中也有用`n`表示的

- **quality** - also known as quality of assessment. This is how difficult (as defined by the user) a flashcard is. The scale is from `0` to `5`.

  此参数表示学习质量，数字越大质量越高越困难，范围是`0`-`5`

- **easiness** - this is also referred to as the easiness factor or EFactor or EF. It is multiplier used to increase the "space" in spaced repetition. The range is from `1.3` to `2.5`.

  这也称为易用性因子或EFactor或EF。 它是用于增加间隔重复中“空间”的乘数。 范围是1.3到2.5

  ==注：==不太懂

- **interval** - this is the length of time (in days) between repetitions. It is the "space" of spaced repetition.

  此参数表示间隔的时间长度，以天为单位

- **nextPractice** - This is the [date/time](https://stackoverflow.com/questions/5175728/how-to-get-the-current-date-time-in-java) of when the flashcard comes due to review again.

  此参数表示下次评估的时间

## 默认参数值

```java
int repetitions = 0;
int interval = 1;
float easiness = 2.5;
```

## 代码实现

```java
private void calculateSuperMemo2Algorithm(FlashCard card, int quality) {

    if (quality < 0 || quality > 5) {
        // throw error here or ensure elsewhere that quality is always within 0-5
    }

    // retrieve the stored values (default values if new cards)
    int repetitions = card.getRepetitions();
    float easiness = card.getEasinessFactor();
    int interval = card.getInterval();

    // easiness factor
    easiness = (float) Math.max(1.3, easiness + 0.1 - (5.0 - quality) * (0.08 + (5.0 - quality) * 0.02));

    // repetitions
    if (quality < 3) {
        repetitions = 0;
    } else {
        repetitions += 1;
    }

    // interval
    if (repetitions <= 1) {
        interval = 1;
    } else if (repetitions == 2) {
        interval = 6;
    } else {
        interval = Math.round(interval * easiness);
    }

    // next practice 
    int millisecondsInDay = 60 * 60 * 24 * 1000;
    long now = System.currentTimeMillis();
    long nextPracticeDate = now + millisecondsInDay*interval;

    // Store the nextPracticeDate in the database
    // ...
}
```

## 有用的链接

+ [StackOverFlowSpaced repetition algorithm from SuperMemo (SM-2)](https://stackoverflow.com/questions/49047159/spaced-repetition-algorithm-from-supermemo-sm-2)
+ [[A Better Spaced Repetition Learning Algorithm: SM2+](http://www.blueraja.com/blog/477/a-better-spaced-repetition-learning-algorithm-sm2)]
+ [github-SaneMemo-python实现](https://github.com/Jakobovski/SaneMemo)
+ [github-anki-optimizer](https://github.com/PhearTheCeal/anki-optimizer)