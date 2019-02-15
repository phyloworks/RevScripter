# Data

### Datatype (Dropdown)

- Nucleotide
		
		num_char_states <- 4

- Amino Acid

		num_char_states <- 20

# Substitution Model
		
### Q Matrix

#### (Nucleotide)

- Model (dropdown)
	- Jukes-Cantor
		
			Q <- fnJC(num_char_states)
		
	- F81
		- Base frequencies
			- Fixed => Enter `pi` simplex vector values (default = (1/4,1/4,1/4,1/4))
			
					pi <- v(<value>, <value>, <value>, <value>)
			
			- Estimate
				- Dirichlet prior distribution => Enter concentration parameters > 0 (default = (1,1,1,1))
		
						pi ~ dnDirichlet(v(<value>, <value>, <value>, <value>))
						moves.append(mvBetaSimplex(pi))
						moves.append(mvDirichletSimplex(pi))
						
		```
		Q := fnF81(pi)
		```
						
	- K80
		- Transition/transversion ratio
			- Fixed => Enter `kappa` value > 0 (default = 1)
			
					kappa <- <value>
			
			- Estimate
				- Prior distribution
					- Exponential => enter `lambda_kappa` rate parameter > 0
					
							lambda_kappa <- <value>
							kappa ~ dnExp(lambda_kappa)
							moves.append(mvScale(kappa))
							
					- Other priors?
						
		```
		Q := fnK80(kappa)
		```
	
	- HKY
		- Transition/transversion ratio
			- Fixed => Enter `kappa` value > 0 (default = 1)
			
					kappa <- <value>
			
			- Estimate
				- Prior distribution
					- Exponential => enter `lambda_kappa` rate parameter > 0
					
							lambda_kappa <- <value>
							kappa ~ dnExp(lambda_kappa)
							moves.append(mvScale(kappa))
							
					- Other priors?
		- Base frequencies
			- Fixed => Enter `pi` simplex vector values (default = (1/4,1/4,1/4,1/4))
			
					pi <- v(<value>, <value>, <value>, <value>)
			
			- Estimate
				- Dirichlet prior distribution => Enter concentration parameters > 0 (default = (1,1,1,1))
		
						pi ~ dnDirichlet(v(<value>, <value>, <value>, <value>))
						moves.append(mvBetaSimplex(pi))
						moves.append(mvDirichletSimplex(pi))
						
		```
		Q := fnHKY(kappa,pi)
		```
		
	- GTR
		- Exchangeabilities
			- Fixed => Enter `er` simplex vector values (default = (1,1,1,1))
			
					er <- v(<value>, <value>, <value>, <value>)
			
			- Estimate
				- Dirichlet prior distribution => Enter concentration parameters > 0 (default = (1,1,1,1))
		
						er ~ dnDirichlet(v(<value>, <value>, <value>, <value>, <value>, <value>))
						moves.append(mvBetaSimplex(er))
						moves.append(mvDirichletSimplex(er))
						
		- Base frequencies
			- Fixed => Enter `pi` simplex vector values (default = (1/4,1/4,1/4,1/4))
			
					pi <- v(<value>, <value>, <value>, <value>)
			
			- Estimate
				- Dirichlet prior distribution => Enter concentration parameters > 0 (default = (1,1,1,1))
		
						pi ~ dnDirichlet(v(<value>, <value>, <value>, <value>))
						moves.append(mvBetaSimplex(pi))
						moves.append(mvDirichletSimplex(pi))
						
		```
		Q := fnGTR(er,pi)
		```
	
#### (Amino acid)
				
- Matrix type (radio button)
	- Empirical
		- Base frequencies (radio button)
			- Empirical
			- Estimated
				- Dirichlet prior distribution => Enter concentration parameter > 0 (default = 1)
			
						pi ~ dnDirichlet(rep(<value>,20))
						moves.append(mvBetaSimplex(pi))
						moves.append(mvDirichletSimplex(pi))
						
		- Model (dropdown)
			- WAG
				
				(Empirical base freqs)
				
					Q <- fnWAG()
				
				(Estimated base freqs)
				
					Q <- fnWAG(pi)
					
			- LG
			
				(Empirical base freqs)
				
					Q <- fnLG()
				
				(Estimated base freqs)
				
					Q <- fnLG(pi)
					
			- etc.
			
	- Estimated
		- Model (dropdown)
			- Poisson
			- GTR
		
### Site Rates Model (Checkboxes)

- +I (Proportion of invariant sites)
	- Fixed => Enter `pinv` value between 0 and 1
		
			pinv <- <value>
	
	- Estimate
		- Beta prior distribution => enter `alpha`, `beta` values > 0 (default = 1,1)
			
				alpha <- <value>
				beta <- <value>
				pinv ~ dnBeta(alpha,beta)
				moves.append(mvBetaSimplex(pinv))
				
- +G (Gamma distributed rates across sites)
	- number of discrete rate categories `k` > 0 (default = 4)
	
			k <- <value>
			
	- shape parameter `shape`
		- Fixed => enter `shape` value > 0
		
				shape <- <value>
			
		- Estimate
			- Prior distribution
				- Exponential => enter `lambda_shape` rate parameter > 0
				
						lambda_shape <- <value>
						shape ~ dnExp(lambda_shape)
						moves.append(mvScale(shape))
						
				- Other priors?
				
	```
	site_rates := fnDiscretizeGamma(shape, shape, k)
	```


# Tree Model

- Topology
	- Unrooted
		- Prior distribution
			- Uniform
			- others?
	- Rooted
		- Prior distribution
			- Yule
			- Birth-death
			- etc.
- Constraints
- Calibrations

# Branch Length/Rate Model

# MCMC