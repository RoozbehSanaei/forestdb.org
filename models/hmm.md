---
layout: model
title: Hidden Markov Model
model-status: code
model-category: Machine Learning
model-tags: temporal models
---

A simple model of a sequence of unobserved states, each of which
depending only on the previous one, and each of which gives rise to
an observation.

    (define (sample-state state)
      (cond
       ((eq? state 0) (sample-discrete '(0.7 0.2 0.1)))
       ((eq? state 1) (sample-discrete '(0.3 0.3 0.4)))
       ((eq? state 2) (sample-discrete '(0.3 0.65 0.05)))))
    
    (define (observe-state state)
      (cond
       ((eq? state 0) (sample-integer 3))
       ((eq? state 1) (+ (sample-integer 3) 1))
       ((eq? state 2) (+ (sample-integer 2) 2))))
    
    (define (hmm state n)
      (if (= n 0)
          '()
          (pair (observe-state state)
                (hmm (sample-state state) (- n 1)))))
    
    (hmm 0 5)