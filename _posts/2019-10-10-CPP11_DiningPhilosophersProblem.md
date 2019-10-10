---
layout: post
excerpt_separator: <!--more-->
title: "C++11 - Solution to Dining Philosophers Problem"
date: 2019-10-10
tags: C++11 programming algorithms
---

__Question:__
Problem states that K philosophers seated around a circular table with one chopstick between each pair of philosophers. There is one chopstick between each philosopher. A philosopher may eat if he can pickup the two chopsticks adjacent to him. One chopstick may be picked up by any one of its adjacent followers but not both.<!--more-->

Eating is not limited by the remaining amounts of spaghetti or stomach space; an infinite supply and an infinite demand are assumed.

The problem is how to design a discipline of behavior (a concurrent algorithm) such that no philosopher will starve; i.e., each can forever continue to alternate between eating and thinking, assuming that no philosopher can know when others may want to eat or think.

![Dining Philosophers](https://media.geeksforgeeks.org/wp-content/uploads/dining_philosopher_problem.png)

__Solution:__

Here is C++11 based solution for the Dining Philosophers Problem:

```C++
#include <iostream>
#include <mutex>
#include <thread>

using namespace std;

int main()
{
    const int no_of_philosophers = 20;
    
    struct Chopstics
    {
    public:
        Chopstics(){;}
        std::mutex mu;
    };
    
    auto eat = [](Chopstics &left_chopstics, Chopstics& right_chopstics, int philosopher_number) {
        
        std::unique_lock<std::mutex> llock(left_chopstics.mu);
        std::unique_lock<std::mutex> rlock(right_chopstics.mu);
        
        cout << "Philosopher " << philosopher_number << " is eating" << endl;
        
        std::chrono::milliseconds timeout(1500);
        std::this_thread::sleep_for(timeout);
        
        cout << "Philosopher " << philosopher_number << " has finished eating" << endl;
    };
    
    //create chopstics
    Chopstics chp[no_of_philosophers];
    
    //create philosophers
    std::thread philosopher[no_of_philosophers];
    
    //Philosophers Start reading
    cout << "Philosopher " << (0+1) << " is reading.." << endl;
    philosopher[0] = std::thread(eat, std::ref(chp[0]), std::ref(chp[no_of_philosophers-1]), (0+1));
    
    for(int i = 1; i < no_of_philosophers; ++i) {
        cout << "Philosopher " << (i+1) << " is reading.." << endl;
        philosopher[i] = std::thread(eat, std::ref(chp[i]), std::ref(chp[i-1]), (i+1));
    }
    
    for(auto &ph: philosopher) {
        ph.join();
    }
    
    return 0;
}
```
