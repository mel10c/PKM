---
title: "Rescorla-Wagner Model"
---


#INFO/Primary/Theory #FIELD/Psych/Cog  | [reference](https://en.wikipedia.org/wiki/Rescorla%E2%80%93Wagner_model)

---

==Rescorla-Wagner Model==

- **A [[Classical Conditioning]] model that is based on learning from errors**

---

# Detail

> Does not work for latent inhibition


<img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h71q51b1w3j30vc08mjt1.jpg" width="500">

- *Associative weight* ($W$): a value representing the **strength of association** between a conditioned stimulus (`CS`) and an unconditioned stimulus (`US`)
    ```text
                 0.0    ---------------------------->    1.0
    (no expectation neutral stimulus)                 (certain)
    ```
- Sum of the stimulus weights is the animal’s prediction
- When the prediction is **wrong/error**, the weights are **adjusted**
    - *Error*: difference between expectation and reality
        - $\text{Prediction Error} = Actual \ US\ – \ Expected \ US$
    - *Adjustment*: each active stimulus adjusted by a proportion of Error
        - $\text{Change in stimulus weight} = Learning Rate \times Prediction Error$
        - Learning Rate: constant for how long learning occurs (between $0-1$)
            - By mapping out learning curves
- When error is 0, no learning occurs (asymptote)
- Example: [[Classical Conditioning#Blocking]]
    - <img src="https://tva1.sinaimg.cn/large/008vxvgGgy1h7ht82t2fmj31bg0hggnx.jpg" width="300">


# Thoughts

# Reference

> [Year:: 1972]
>
> [Psychologist:: Robert A. Rescorla, Allan R. Wagner]
>
> [Publish:: ]
>
> [Concept:: [[Classical Conditioning]]]
