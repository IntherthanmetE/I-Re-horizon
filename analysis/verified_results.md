# Verified Results Checkpoint

## Model
- IFM/K2-Horizon-MoVA-36B-A4B
- 48 layers
- hidden_size 2560
- vocab_size 250624
- 100 MoE experts, top-8
- 64 MoVA V-experts, top-4
- layers 0-2 dense
- layers 3-47 sparse MoE + MoVA

## Tensor index
- Total tensors: 16,998
- Total shards: 48
- MoE expert tensors: 16,515
- Attention: 243
- Transformer layer: 99
- Router: 90
- Norm: 49
- Embedding: 1
- LM head: 1

## Tokenizer
- tokenizer.json vocab: 250000
- model vocab_size: 250624
- ดี -> [35789, 34163] -> 2 tokens
- good -> [24405] -> 1 token
- สวัสดี -> 6 tokens
- ภาษาไทย -> [247299, 14744, 173523] -> 3 tokens
- hello -> 1 token
- English -> 1 token

## Tokenization comparison
- Small Thai test average: 7.27 tokens
- Small English test average: 2.33 tokens
- Thai/English token ratio: ~3.11x
- Thai corpus: 297 chars / 209 tokens / 1.421 chars per token

## Layer 0
Shard: model-00001-of-00048.safetensors
Header size: 1360
Data base: 1368
10 tensors:
- input_layernorm.weight [2560]
- mlp.down_proj.weight [2560,6144]
- mlp.gate_proj.weight [6144,2560]
- mlp.up_proj.weight [6144,2560]
- post_attention_layernorm.weight [2560]
- self_attn.gate_proj.weight [4096,2560]
- self_attn.k_proj.weight [1024,2560]
- self_attn.o_proj.weight [2560,4096]
- self_attn.q_proj.weight [4096,2560]
- self_attn.v_proj.weight [1024,2560]

Layer 0 verified statistics:
input_layernorm:
- min 0.15527344
- max 2.25
- mean 0.51087606
- std 0.32667086

attention:
- gate_proj shape (4096,2560), min -0.29101562, max 0.46289062, mean 0.0002564055, std 0.023187201
- k_proj shape (1024,2560), min -0.3515625, max 0.3515625, mean -2.433297e-05, std 0.023381673
- o_proj shape (2560,4096), min -1.3671875, max 1.46875, mean -1.0755333e-06, std 0.022258991
- q_proj shape (4096,2560), min -0.31445312, max 0.28515625, mean 5.3761596e-06, std 0.019602422
- v_proj shape (1024,2560), min -0.23828125, max 0.27929688, mean 2.6900301e-05, std 0.023798214

## Layer 3
Shard: model-00004-of-00048.safetensors
Header size: 46016
Data base: 46024

Tensor count: 377
- MoE experts: 300
- MoE router: 2
- Shared expert: 3
- Attention: 4
- MoVA V-experts: 64
- MoVA router: 2
- LayerNorm: 2

Layer 3 v_router.weight:
- dtype BF16
- shape [64,2560]
- min -0.32226562
- max 22.625
- mean 0.008548295
- std 0.44710058

Layer 3 v_router.bias:
- dtype BF16
- shape [64]
- min -0.03955078
- max 0.06738281
- mean 0.0017409176
- std 0.020751277

## Layer 10 MoE router
Shard: model-00011-of-00048.safetensors

gate.weight:
- shape [100,2560]
- dtype BF16
- min -0.73828125
- max 0.53125
- mean -0.00060322596
- std 0.061602216

gate.bias:
- shape [100]
- dtype BF16
- min 15.1875
- max 15.4375
- mean 15.324375
- std 0.04392376

Router row cosine similarity:
- min 0.11554189
- max 0.584345996
- mean 0.23596624
- std 0.05021353
- highest pair: expert 30 <-> 69, cosine 0.584345996

## Routing verification
Verified K2 routing behavior:
- sigmoid routing logits
- bias affects selection scores
- top-k = 8
- original routing weights gathered
- top-k weights normalized
- multiplied by scaling factor 2.5
- selected weights sum to ~2.5 per token

## Important architecture facts
- Layers 0-2: Dense Attention + Dense FFN
- Layers 3-47: MoVA Attention + Sparse MoE
- MoE: 100 experts, top-8, one shared expert
- MoE expert intermediate size: 768
- Dense FFN intermediate size: 6144
- MoVA: 64 value experts, top-4
- Q heads: 32
- KV heads: 8
- head_dim: 128
- GQA groups: 4
- RoPE head_dim: 128
- attention gate: Softplus
- max context: 524288

## Remote Range reading
Verified HTTP 206 Range reads directly from Hugging Face safetensors.
No full 75 GB model download was required.

## Next checkpoint
Layer 0 FFN weights and post-attention norm remain to be read.
Do not instantiate the full 36B model.
