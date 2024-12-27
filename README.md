# Polynomial Commitment Setup Guide for Passport Data ZK Proof

## Overview
This guide demonstrates how to set up polynomial commitments for zero-knowledge proofs of passport data, where the verifier only needs to confirm the prover knows the data without seeing it.

## 1. Witness Setup (Core Focus)

### 1.1 Passport Data Structure
Convert the four passport data points into field elements:
- `w₁`: Passport Number
- `w₂`: Date of Birth
- `w₃`: Expiry Date
- `w₄`: Document Type Code

### 1.2 Polynomial Construction
1. Create witness polynomial W(x):
   ```
   W(x) = w₁ + w₂x + w₃x² + w₄x³
   ```
2. Generate random blinding factor r
3. Construct blinded polynomial:
   ```
   B(x) = W(x) + r * Z(x)
   ```
   where Z(x) is the vanishing polynomial for the evaluation points

## 2. Commitment Phase

1. Select trusted setup parameters (G₁, G₂)
2. Compute commitment C:
   ```
   C = B(s) * G₁
   ```
   where s is the trusted setup secret

## 3. Proof Generation

1. Create evaluation proof π for points (x₁, ..., x₄)
2. Generate zero-knowledge proof that:
   - Prover knows witness values w₁,...,w₄
   - Values satisfy range constraints for passport data
   - Commitment C matches the witness polynomial

## 4. Verification Protocol

Verifier checks:
1. Commitment validity
2. Proof of knowledge
3. Range proofs for passport data format

## Security Considerations

- Blinding factor ensures zero-knowledge property
- Polynomial degree bound prevents information leakage
- Trusted setup parameters must be securely generated
- Verification doesn't reveal actual passport data

## Implementation Notes

1. Use existing ZK-SNARK libraries for polynomial commitments
2. Implement proper data sanitization for passport inputs
3. Ensure secure parameter generation
4. Maintain separate circuits for commitment and proof generation
