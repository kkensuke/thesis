Script
===


## Page 1 Title
- My research title is "Analysis of Data-encoding Induced Barren Plateau in Quantum Machine Learning"
- I studied the gradient vanishing problem called barren plateau during the optimization process in quantum machine learning.


## Page 2 Table of Contents
- First, I will begin by explaining some fundamental staffs:
    - Quantum Computing
    - Variational Quantum Algorithms
    - Quantum Machine Learning within VQA
    - The gradient vanishing problem known as Barren Plateaus
- Following that, I will present:
    - An overview of my research
    - The achievements of my study


## Page 4 Quantum Computing
- Quantum computations are described using the quantum circuit model, which consists of the following three elements:
        Qubits: Two-level systems called quantum bits.
        Quantum gates that change the state of qubits.
        Measurement operations that extract information from qubits.
- Currently available quantum computers have a limited number of qubits, a few hundred.
- So they can't implement error correction and noise cannot be ignored.
- which means there are limitations on the depth of quantum circuits.
- Thus, they are called Noisy Intermediate-Scale Quantum devices, NISQ for short.


## Page 5 Variational Quantum Algorithms
- However, Variational Quantum Algorithms (VQA) are executed even in quantum computers like NISQ.
- VQA is a hybrid algorithm utilizing both quantum and classical computers.
- VQA use parameterized quantum circuits to generate parameter-dependent quantum states and measure observables with these states.
- The cost function is defined based on the expectation values of these observables.
- The cost function and its gradients are calculated classically to update the parameters, and updated parameters are reinput to the quantum circuit again.
- Iterating this process, the parameters are optimized to minimize the cost function.
- We can apply VQA to various problems by reformulating them as minimization problems.
- It finds applications in many fields like quantum chemistry, combinatorial optimization, and quantum machine learning.


## Page 6 Quantum Machine Learning
- Here, I explain quantum machine learning within the framework of variational quantum algorithms.
- Especially, let's consider solving classification problems in supervised learning using the quantum circuit on the right.
- This circuit consists of an encoding circuit that encodes data into a quantum state and a ansatz that inputs parameters.
- The generated quantum state as a trial function is used to measure an observable, and its expectation value is used as the predicted label.
- A cost function is defined using a error function (f) that returns the difference between the predicted labels and teacher labels.
- function f can be absolute error, squared error, and cross-entropy.


## Page 7 Barren Plateaus
- I've explained variational quantum algorithm and quantum machine learning within that framework.
- However, In these algorithms, there is a known problem called Barren Plateaus, which is a gradient vanishing problem.
- Barren Plateaus occur when the mean of cost function gradient is zero, and the variance of gradients exponentially decays with the number of qubits n.
- For instance, with M measurements, the measurement error is 1 / √M.
- However, in Barren Plateaus, the gradient takes exponentially small values, so the measurement error must also decays exponentially to distinguish the sign of the gradient, positive or negative.
- Thus, we need exponentially many measurements to obtain the gradient, which is impractical.
- So, the scaling the variance of the gradients is important in terms of computational complexity of the algorithm.
- In my research achievements, I derived upper and lower bounds on the variance of the cost function gradient.
- The bottom left figure shows the profile of the cost function for a specific parameter in Barren Plateaus.
- We can see that the cost function becomes flat as we increase the number of qubits n. This flat region is called Barren Plateau.
- The bottom right figure shows the numerical calculation of variance of gradient when using deep quantum circuit, and indeed we can see the exponential decay of the variance.
- Causes of Barren Plateaus include the depth of the ansatz, the locality of the observable, noise (which exacerbates and flattens the entire cost function), and inputting training data into the quantum circuit.
- That concludes the explanation of the background knowledge.


## Page 9 Research Overview
- This is an overview of my research.
- As I explained, we are trying to make quantum machine learning efficient.
- but, during the optimization process, there is a gradient vanishing problem called Barren Plateau.
- and the specific effect of data encoding on BP is not examined well.
- Therefore, my goal was to investigate and mitigate the Barren Plateau in quantum machine learning due to data encoding.
- To this end, I analysed the effect of data encoding on the scaling of the variance of the cost function gradient.
- however, it is difficult to calculate the variance of the gradient exactly, so I derived upper and lower bounds on the variance of the gradient.
- And I numerically verified that the scaling is independent of the specific form of error functions such as absolute error, squared error or cross-entropy error.


## Page 11 Upper Bound on Variance of Gradient: Setup
- First, let me explain the first research findings: the upper bound on the variance of the gradient. (I explained this part 2 months ago, but I will explain from the beginning)
- On this page, I will describe the setup of the quantum circuit used in deriving the upper bound.
    - The quantum circuit consists of an encoding circuit in blue and an ansatz in red.
    - The state after the encoding circuit is denoted as ρ_i, which is called input state.
    - the state after the ansatz is denoted as ρ_i(θ).
    - The ansatz is made up of s-qubit unitary blocks, and there are ξ such blocks, so n = s times ξ qubits in a total
    - we assume that the parameter to take the gradient is in the h-th s-qubit unitary of the ansatz.
    - The contraction of the input state entering the hth s qubits is described as ρ_i^h.
    - The observable is defined like this, and the predicted label \ell_i is its expectation value, taking between 0 and 1.
    - The parameters of the ansatz are randomly initialized, and each s-qubit unitary is assumed to have the random property of unitary 2-design.
    - In this setup, the ansatz and the observable are defined to avoid Barren Plateaus.
## Page 12 Upper Bound on Variance of Gradient: Results
- Under the these settings, I derived the upper bound on the variance of the gradient in binary classification
- y_i is the teacher label, taking 0 or 1.
- The cost function is defined as the average difference between the teacher labels and predicted ones for all data.
- When using the quantum circuit described earlier, the upper bound on the variance of the gradient is given as follows.
- The upper bound consists of three elements' product.
    - The first element, A_f, is determined by the form of the function f, such as squared error.
    - The second element, r_n,s, is determined by the observable.
    - The last element, D_HS, is affected by the input states.
    - The rightmost term in the inequality is an upper bound on D_HS. First term decays exponentially and second term is called expressibility. When the encoding circuit is expressive, the value of expressibility is small, leading to a small upper bound.
    - If the entire encoding circuit have the random property of unitary 2-design, which means too expressive, the value of expressibility becomes 0. So, the upper bound consists only of exponentially decaying term, leading to Barren Plateau.
    - However, assuming that the entire encoding circuit is unitary 2-design requires very deep quantum circuit. So, here, I don't use this strong assumption and analyze the behavior of the upper bound as the layer number increases from shallow to deep, from the viewpoint of the encoding circuit.
## Page 13 Upper Bound on Variance of Gradient: Specific encoding circuit Structure
- For the analysis, I used the Alternating Layered Ansatz for the encoding circuit, which is in blue. The red blocks are the ansatz with parameters.
- The number of layers is defined by the number of dashed lines.
- Here, I calculate D_HS, assuming that each blue unitary block, has the random property of a unitary 2-design, not the entire encoding circuit.
## Page 14 Comparison of Variance of Gradient and its Upper Bound
- Under these assumptions, I calculated and plotted the upper bound on the right.
- The x axis is the number of layers (L) in the encoding circuit, and the plot shows the values of the upper bound as the number of layers increases. Each color corresponds to a different number of qubits (2, 4, 6, 8).
- The dashed lines are convergent values when the circuit is deep enough, in other words, they are the upper bound when the entire encoding circuit is unitary 2-design. dashed lines in the left are the same as the right.
- and, the left figure is the variance of gradients by quantum circuit simulations using the Iris dataset and a blue block structure composed of Rx, Ry, and CNOT.
- Indeed, the right figure is working as upper bound on the variance of the gradient.
## Page 15 necessary condition for the Number of encoding Layers
- On the previous page, I showed a plot including all elements of the upper bound. But, here, I especially focus on D_HS and plot it alone here.
- It is obvious from the plot that D_HS does not fall below a certain line.
- Remember that D_HS should not exhibit exponential decay to avoid Barren Plateau. So, the line should be larger than a polynomial of the number of qubits, n.
- Thus, the number of layers in encoding circuit (L) should be  order log(n).
- This is the necessary condition to avoid Barren Plateau.
- It concludes the research finding on the upper bound.


- Next, I move on to the lower bound on the variance of the gradient.
## Page 17 Lower Bound on the Variance of Gradient: Setup
- In the upper bound section, we understood when the variance becomes small.
- Here, I will show the lower bound on the variance of the gradient to understand when the variance becomes large.
- First, let me explain the settings for deriving the lower bound.
- The encoding circuit is in blue, and the ansatz is in red.
- The ansatz consists of s-qubit unitary blocks, and there are ξ such blocks. The same as before, parameters are randomly initialized, and each block is unitary 2-design.
- so, there are s times ξ qubits.
- For simplicity, I used the encoding circuit consists of L layers of only R_y gates.
- We consider a binary classification again, and we choose mean absolute error as the cost function. We will discuss other error functions later.
- Here, we have two input datasets X for label 0 and Z for label 1 with a size ratio p to q
- Each element of the input data follows Gaussian distribution, and maximum variance is denoted by σ_max
## Page 18 Lower Bound on the Variance of Gradient: Results
- Under these settings, the lower bound on the variance of the gradient is given as follows.
- p and q represent the size ratio of the datasets for each label.
- \Sigma_x|j, \Sigma_z|j is the sum of variances of input data to the j-th qubit. The sum is taken over depth index d.
- Especially when the size ratio of the datasets is 1 to 1, or p and q equals 1/2, the lower bound is as follows.
- As you can see, the lower bound becomes larger when there is a large difference between the variances of the input data.
- However, as the number of encoding layers L increases, both e^-\Sigma_x|j and e^-\Sigma_z|j generally decays exponentially. Therefore, the lower bound also decays exponentially.
- And, if e^-\Sigma_x|j = e^-\Sigma_z|j for all index j, the lower bound becomes 0. In the extreme case of dataset X, Z are the same dataset, the cost function here becomes constant, which means the variance of the gradient is 0. So, the lower bound can be 0.
## Page 19 Lower Bound on the Variance of Gradient: Results
- As another example, let's consider the case where the size ratio of the datasets is 1 to 0.
- This corresponds to one-class classification problems, which is used in anomaly detection. I'm not so much familiar with though ...
- anyway, in this case, p is 1, q is 0, and the lower bound on the variance of gradient is simplified as follows.
- From this, you can see that if (s) and (L\sigma_\max^2) are the order of log(n) the lower bound is polynomial of the number of qubits n, thus avoiding Barren Plateau. This is a sufficient condition to avoid Barren Plateau in this case.
- These are the research findings on the lower bound on the variance of the cost function gradient.


## Page 22 Form of the Error Function and Scaling of the Variance of Gradient
- In the analysis of the scaling of the lower bound, we used the absolute error of the cost function for simplicity. However, in practice, mean squared error (MSE) and cross-entropy error are commonly used. So, we consider the scaling of the variance of the gradient for these error functions. The conclusion is that the scaling of the variance of the gradient for mean squared error and cross-entropy error is numerically confirmed to be similar to that of absolute error.
- Three functions are defined as follows.
- The gradients for these error functions are as follows. Here, the gradients are transformed to compare with the absolute error,
- and you can see the gradient of MSE and LOG have coefficients, which depend on absolute value of (\ell_i - y_i).
## Page 23 Form of the Error Function and Scaling of the Variance of Gradient
- Now, this is quite sudden, but, let's assume that the red ansatz is sufficiently deep, or unitary 2-design. In this case, the mean of \ell_i is 1/2, and the variance exponentially decays with the number of qubits n. That is, it exponentially concentrates around 1/2.
- So, I assume that \ell_i is approximately 1/2 for all i, and absolute value of (\ell_i - y_i) can also be approximated as 1/2.
- Then, from the previous expression, the gradients for mean squared error and cross-entropy error are about 1 times and 2 times the gradient for the absolute error.
- Thus, the variance scaling of the gradients for mean squared error and cross-entropy error is approximately 1 times and 4 times the scaling of the variance of the gradient for the absolute error.
- So under the assumption of sufficient deep ansatz, the scaling of the variance of the gradient for mean squared error and cross-entropy error is similar to the scaling the absolute error.
## Page 24 Form of the Error Function and Scaling of the Variance of Gradient
- In the previous page, we approximately showed that the scaling of the variance of the gradient is similar for deep ansatz.
- Now, we consider whether this scaling similarity is also valid for shallow ansatz.
- We use Tensor Product for the encoding circuit and the Alternating Layered Ansatz for the ansatz, and we computed the variance of the gradients for each error function.
- (next page) These are the results of the numerical calculation of the variance of the gradient for each error function. And x axis is the number of layers in the ansatz, and y axis is the variance of the gradient. Using these results, we calculated the ratio of the variance of the gradient.
## Page 25 Form of the Error Function and Scaling of the Variance of Gradient
- These are the results.
- The left plot shows the ratio of the variances of MSE to MAE, and the right plot shows cross-entropy (LOG) to MAE.
- The x axis is the number of layers in the ansatz, and y axis is the ratio of the variances of the gradients.
- The dashed lines is the approximate ratios obtained earlier (1 and 4).
- you can see even when the ansatz is shallow, the ratio of the variances of the gradients is close to the approximate values. In the case of n is 2, plot is a bit away from the dashed line. I think this is because the approximation does not hold since the variance of \ell_i is large when n is small
- Therefore, the result obtained in the lower bound for the scaling of the variance of the gradient for the absolute error can be applied to the scaling of the variance of the gradient for mean squared error and cross-entropy error.


## Page 27 Summary
- Summary:
  - In this study, I investigated the effect of data encoding on Barren Plateau.
  - First, we derived and numerically verified the upper bound on the variance of the gradient from the perspective of data encoding.
  - We observed that the entanglement of the state after data encoding and the expressibility of the encoding circuit are important → leading to a small upper bound, or Barren Plateau.
  - Additionally, if the number of layers of encoding circuit is order of \log{n}, the upper bound does not decay exponentially.
  - I also showed that When input data follows Gaussian distribution, the variance of input data is crucial for the lower bound on the variance of gradient.
  - Finally, we numerically confirmed that the scaling of the variance of the gradient is almost independent of the form of the error function.
- As future work, I would like to consider the following:
  - First, investigating the lower bound for more general encoding circuits.
  - Second is to consider the encoding circuit from the perspective of generalization performance.
  - and finally, I said that the depth of the circuit need to be order of log{n} to avoid Barren Plateau, but just too shallow quantum circuit can be classically simulated.
  - So, it is also important to examine whether the encoding circuit becomes classically hard to simulate in terms of computational complexity.