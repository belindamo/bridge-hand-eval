# Monte Carlo Methods for Bridge

## Perfect Information Monte Carlo (PIMC)

### Core Algorithm (Levy, 1989; Ginsberg, 2001)
**Basic Approach**: Sample possible card distributions, solve as perfect information game
- **Assumption**: Random sampling of hidden cards provides representative scenarios
- **Method**: For each sample, use minimax/alpha-beta on complete information
- **Success**: Widely adopted in commercial bridge programs (GIB, WBridge5)

### Fundamental Problems Identified

#### Strategy Fusion (Frank & Basin, 1998)
**Problem**: PIMC can't distinguish between different information sets
- **Example**: Playing different cards from same information set across samples
- **Impact**: Leads to suboptimal strategies that would be impossible for humans
- **Core Issue**: Algorithm "cheats" by using future perfect information

#### Non-Locality (Frank & Basin, 1998)  
**Problem**: Node values depend on external subtree information
- **Impact**: Makes tree search beyond depth 2 very difficult
- **Consequence**: Limited depth analysis in complex positions

## Advanced Monte Carlo Variants

### αμ Search (Cazenave & Ventos, 2019)
**Innovation**: Anytime heuristic search for incomplete information games
- **Key Insight**: Assumes perfect information for opponents while preserving incomplete info for player
- **Advantage**: Addresses strategy fusion and non-locality problems
- **Method**: Uses partial orders and vector-valued evaluations
- **Application**: Successfully applied to bridge endgame solving

### Recursive Monte Carlo (Bouzy et al., 2020)
**Breakthrough**: First successful recursive application to bridge cardplay
- **Method**: Level N+1 RMC uses Level N RMC as simulator
- **Results**: Level-1 RMC outperforms standard MC by 0.5 trick per distribution
- **Innovation**: Eliminates dependence on domain-specific double dummy solver
- **Cost**: Exponential increase in computation time per recursion level

### Information Set Monte Carlo Tree Search (ISMCTS)
**Development**: Cowling, Powley & Whitehouse (2012)
- **Innovation**: Searches trees of information sets rather than game states
- **Advantage**: Directly analyzes true game structure under imperfect information
- **Applications**: Successfully applied to various card games including bridge variants
- **Commercial Success**: Integrated into Spades by AI Factory (2.5M+ downloads)

## Sampling and Determinization Issues

### Perfect Information Monte Carlo Problems

#### Overconfidence in Hidden Information
**Issue**: PIMC assumes opponent knowledge of hidden cards in future states
- **Solution**: Presumed Value PIMC (Wisser, 2015)
- **Method**: Adjusts for overestimation of opponent information
- **Result**: Expert-level performance in Schnapsen card game

#### Sample Distribution Bias
**Problem**: Uniform sampling may not reflect actual game distributions
- **Research**: Long et al. (2010) identified game properties affecting PIMC performance
- **Finding**: PIMC performance varies dramatically based on game tree structure
- **Implication**: Need for adaptive sampling strategies

### Extended PIMC (EPIMC)
**Innovation**: Arjonilla et al. (2024) - postpones perfect information resolution
- **Method**: Delays leaf evaluation to reduce strategy fusion effects
- **Results**: Notable performance improvements in games with high strategy fusion
- **Theoretical Contribution**: Enhanced understanding of determinization-based algorithms

## Assumptions Across Monte Carlo Literature

1. **Random Distribution**: Hidden cards are uniformly distributed among unknown players
2. **Independence**: Each sample provides independent information about optimal play
3. **Representativeness**: Finite sampling adequately represents full distribution
4. **Perfect Play**: Opponents play optimally in sampled scenarios
5. **Static Evaluation**: Hand strength doesn't change based on bidding information

## Current Limitations

1. **Computational Cost**: Recursive methods require exponential time increases
2. **Strategy Fusion**: Still affects most PIMC variants
3. **Bidding Integration**: Limited application to bidding phase of bridge
4. **Partnership Cooperation**: Difficulty modeling cooperative gameplay in incomplete information