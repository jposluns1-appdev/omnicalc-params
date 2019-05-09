# Omnicalc `params`

Dynamic web applications are more interesting than static websites for one reason: **user input.** Let's finally learn how to let our users give us input!

### [Here is the target we will ultimately build.](https://omnicalc-params.herokuapp.com/)

## Setup

 1. From [your Cloud9 repositories list](https://c9.io/account/repos), set up a workspace [as usual](https://guides.firstdraft.com/starting-on-a-project-in-cloud9).
 1. Set up the project: `bin/setup`
 1. Start the web server by clicking "Run Project".
 1. Navigate to your live application preview.
 1. You'll see the standard "You're on Rails" welcome page for a brand new, blank Rails application.
 1. As you work, remember to navigate to `/git` often and **always be committing.**
 1. `rails grade` when you're ready for feedback.

## Part I: Flexible Routes

### Square with flexible path segment

If I visit a URL of the pattern

```
/flexible/square/:number
```

I should see the square of the number in the third segment of the path. I should be able to enter any _integer_ in the third segment of the path; but not a decimal number (since you can't put dots in the middle of URLs).

#### Example

If I visit [http://localhost:3000/flexible/square/5](http://localhost:3000/flexible/square/5), I should see something like

> ## Flexible Square
>
> The square of 5 is 25.

### Square Root with flexible path segment

If I visit a URL of the pattern

```
/flexible/square_root/:number
```

I should see the square root of the number in the third segment of the path. I should be able to enter any _integer_ in the third segment of the path; but not a decimal number (since you can't put dots in the middle of URLs).

#### Example

If I visit [http://localhost:3000/flexible/square_root/8](http://localhost:3000/flexible/square_root/8), I should see something like

> ## Flexible Square Root
>
> The square root of 8 is 2.8284271247461903.

### Payment with flexible path segments

If I visit a URL of the pattern

```
/flexible/payment/:basis_points/:number_of_years/:present_value
```

I should see the **monthly** payment due, assuming that:

 - The integer in the third segment of the path is an _annual_ interest rate _in basis points_, or hundredths of a percent.
 - The integer in the fourth segment of the path is the number of _years_ remaining.
 - The integer in the fifth segment of the path is the present value.
 - Use this formula to calculate the payment:

    ![Payment formula](payment_formula.gif?raw=true "Payment formula")

    (The image of the formula above will only render if you're viewing this README on GitHub.com. Alternatively, the image is located at `/payment_formula.gif` in the repository.)

#### Example

If I visit [http://localhost:3000/flexible/payment/410/30/250000](http://localhost:3000/flexible/payment/410/30/250000), I should see something like

> ## Flexible Payment
>
> A 30 year loan of $250,000, with an annual interest rate of 4.10%, requires a monthly payment of $1,208.00.

### Random with flexible path segments

If I visit a URL of the pattern

```
/flexible/random/:min/:max
```

I should see a random number that falls between the integers in the third and fourth segments of the path.

#### Example

If I visit [http://localhost:3000/flexible/random/50/100](http://localhost:3000/flexible/random/50/100), I should see something like

> ## Flexible Random Number
>
> A random number between 50 and 100 is 87.

### Notes for flexible path segment tasks

**All of the above should work no matter what integers I type into the flexible segments of the path.**

Remember:

 - **Rails places all user input in the `params` hash.**
 - You can use the `params` hash in your actions or your views as you would any `Hash`; `.keys`, `.fetch`, etc.
 - Watch the server log to see what the `params` hash contains for any given request.

#### Your task: Build out flexible RCAVs so that all of these (infinitely many) URLs work.

## Part II: Forms

Now, let's build something a little more realistic. **Our users don't want to type input into the address bar; they want to type into forms!**

The way it should work is:

 - If I visit the URL [http://localhost:3000/square/new](http://localhost:3000/square/new), I should see a form with a label and an input to enter a number. (Since we're no longer typing into the address bar, we can use decimals and are no longer limited to integers. Yay!)
    - If I submit that form, I should see the square of the number that I entered.
 - If I visit the URL [http://localhost:3000/square_root/new](http://localhost:3000/square_root/new), I should see a form with a label and an input to enter a number.
    - If I submit that form, I should see the square root of the number that I entered.
 - If I visit the URL [http://localhost:3000/payment/new](http://localhost:3000/payment/new), I should see a form with labels and inputs to enter three values:
    - An APR (annual percentage rate). (Since our users are no longer limited to integers, we can avoid thinking in basis points. Phew!)
    - A number of _years_ remaining
    - The principal
    - If I submit that form, I should see the **monthly** payment due given the values that I entered.
 - If I visit the URL [http://localhost:3000/random/new](http://localhost:3000/random/new), I should see a form with labels and inputs to enter two numbers, a minimum and a maximum.
    - If I submit that form, I should see a random number that falls between the numbers that I entered.
