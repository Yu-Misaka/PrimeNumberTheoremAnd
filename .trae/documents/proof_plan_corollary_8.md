# Corollary 8 证明计划

## 整体目标
证明 `corollary_8`，即对任意 `x ≥ x₁`，有 `Eπ x` 小于等于所有区间上 `επ_num` 的上确界。

## 证明思路回顾
1. 找到包含 `log x` 的区间 `[b' i, b' (i+1)]`
2. 对该区间应用 `theorem_6` 得到局部界
3. 利用上确界性质得到全局界

---

## 子目标拆分

### 子目标 1：找到合适的索引 `i`
- 给定 `x ≥ x₁`，找到 `i : Finset.Iio (Fin.last M)`，使得 `(b' i).toReal ≤ log x` 且 `log x ≤ (b' (i+1)).toReal`（或当 `i+1 = Fin.last M` 时无上限）
- 需要利用 `b'` 的单调性和覆盖性

### 子目标 2：验证 `theorem_6` 的条件
对于选中的 `i`，构造局部参数并验证：
- `x₀' := x₁`（推论中的 `x₁` 作为定理6中的 `x₀`）
- `x₁' := exp (b' i).toReal`
- `x₂' := if (i+1) = Fin.last M then ⊤ else exp (b' (i+1)).toReal`
- 验证 `h' : x₁' ≥ max x₀' 14`
- 构造局部划分 `b_local`
- 验证局部划分的单调性和端点条件

### 子目标 3：应用 `theorem_6`
- 对构造的参数应用 `theorem_6`，得到 `Eπ x ≤ επ_num b_local εθ_num x₀' x₁' x₂'`

### 子目标 4：连接到 `iSup`
- 证明 `επ_num b_local εθ_num x₀' x₁' x₂'` 等于 `iSup` 定义中对应 `i` 的项
- 利用 `le_iSup` 性质，得到该项 ≤ `iSup (fun i ↦ ...)`

### 子目标 5：传递性得到结论
- 结合子目标 3 和 4，由传递性得到 `Eπ x ≤ iSup (fun i ↦ ...)`

---

## 技术要点

1. **EReal 的处理**：`b'` 是 `EReal` 类型的划分，需要处理 `toReal` 转换
2. **划分索引**：`Fin (M + 1)` 的索引操作，特别是 `Fin.last M`
3. **局部划分构造**：从 `b'` 的前 `i.val.val+1` 个点构造 `Fin (i.val.val+1) → ℝ` 类型的划分
4. **单调性传递**：从 `hmono : Monotone b'` 得到局部划分的单调性

---

## 下一步
计划确认后，将逐个实现上述子目标。
