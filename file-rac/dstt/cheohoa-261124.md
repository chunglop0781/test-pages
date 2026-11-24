# Chéo hóa ma trận: hai ví dụ có cùng trị riêng 2 (hai lần)

Tài liệu này so sánh hai ma trận 2×2 có **cùng trị riêng** nhưng một ma trận chéo hóa được, ma trận kia thì không. Cuối tài liệu có code Python để kiểm tra bằng số và vẽ hình.

## 1. Ý tưởng cần nhớ

- **Hướng riêng** của A là hướng mà A không làm xoay, chỉ kéo dài hoặc co lại: `A·v = λ·v`. Hệ số `λ` gọi là **trị riêng**.
- Ma trận n×n **chéo hóa được** khi có đủ **n hướng riêng độc lập**. Khi đó đổi sang các hướng này làm trục thì A chỉ còn kéo giãn từng trục (dạng ma trận chéo).
- Với một trị riêng λ, số hướng riêng độc lập của nó là:

```
số hướng riêng = n − rank(A − λI)
```

- Nếu trị riêng λ xuất hiện k lần mà chỉ có ít hơn k hướng riêng thì A **không** chéo hóa được.

## 2. Ví dụ 1: chéo hóa được

```
A = [ 2  0 ]
    [ 0  2 ]
```

**Bước 1: trị riêng.**
`det(A − λI) = (2 − λ)² = 0` nên `λ = 2` (hai lần). Cần 2 hướng riêng.

**Bước 2: giải (A − 2I)v = 0.**

```
A − 2I = [ 0  0 ]      [ 0  0 ] [ x ]   [ 0 ]
         [ 0  0 ]      [ 0  0 ] [ y ] = [ 0 ]
```

Phương trình luôn đúng với mọi x, y. Chọn `v1 = (1, 0)` và `v2 = (0, 1)`: có 2 hướng riêng độc lập.
Kiểm tra bằng công thức: `rank(A − 2I) = 0` nên số hướng riêng = 2 − 0 = 2.

**Bước 3: hình.** Cả hai trục chỉ bị kéo dài 2 lần, không đổi hướng.

**Kết luận:** cần 2 hướng, có 2 hướng, nên A **chéo hóa được**.


<img width="1194" height="606" alt="image" src="https://github.com/user-attachments/assets/34eae26e-c8b1-4e56-b1b4-58a40c7a25fd" />


## 3. Ví dụ 2: không chéo hóa được

```
B = [ 2  1 ]
    [ 0  2 ]
```

**Bước 1: trị riêng.**
`det(B − λI) = (2 − λ)² = 0` nên `λ = 2` (hai lần). Cần 2 hướng riêng, giống ví dụ 1.

**Bước 2: giải (B − 2I)v = 0.**

```
B − 2I = [ 0  1 ]      [ 0  1 ] [ x ]   [ y ]   [ 0 ]
         [ 0  0 ]      [ 0  0 ] [ y ] = [ 0 ] = [ 0 ]
```

Hàng 1 cho `y = 0`, còn x tự do. Chỉ có `v = (1, 0)`, nằm trên trục ngang: **1 hướng riêng**.
Kiểm tra bằng công thức: `rank(B − 2I) = 1` nên số hướng riêng = 2 − 1 = 1.

**Bước 3: hình.** Trục ngang vẫn chỉ bị kéo dài 2 lần. Trục đứng `e2 = (0, 1)` bị biến thành `B·e2 = (1, 2)`, tức là bị nghiêng đi, nên không phải hướng riêng.

**Kết luận:** cần 2 hướng, chỉ có 1 hướng, nên B **không chéo hóa được**.

<img width="1194" height="606" alt="image" src="https://github.com/user-attachments/assets/eaa2948a-d5cd-4c6b-81a0-b3ad93f81c0f" />

## 4. So sánh nhanh

| | Ví dụ 1 (A) | Ví dụ 2 (B) |
|---|---|---|
| Trị riêng | 2, 2 | 2, 2 |
| Ma trận A − 2I | toàn 0 | có số 1 ở ô (1,2) |
| rank(A − 2I) | 0 | 1 |
| Số hướng riêng của λ = 2 | 2 | 1 |
| (A − 2I) = 0 ? | đúng | sai |
| Chéo hóa được | có | không |

Trị riêng giống nhau nên định thức và `det(A − I)` cũng giống nhau, không phân biệt được hai ví dụ. Thứ phân biệt là số 1 nằm giữa hai cột cùng trị riêng.

## 5. Phép thử tích (A − λ₁I)(A − λ₂I)…

Nhân các `(A − λI)` theo **từng trị riêng khác nhau** (mỗi trị riêng một lần):

- Tích bằng ma trận 0 thì A chéo hóa được.
- Tích khác 0 thì A không chéo hóa được.

Lý do: tích bằng 0 nghĩa là đa thức `(x − λ₁)(x − λ₂)…` (không có nghiệm lặp) triệt tiêu A, và điều đó tương đương với A chéo hóa được.

Áp dụng cho bài 3×3:

```
C = [ 2  1  0 ]        trị riêng: 2, 2, 3
    [ 0  2  0 ]
    [ 0  0  3 ]

(C − 2I)(C − 3I) = [ 0  -1  0 ]
                   [ 0   0  0 ]  ≠ 0
                   [ 0   0  0 ]
```

Tích khác 0 nên C không chéo hóa được. Số 1 ở ô (1,2) nằm giữa hai cột cùng trị riêng 2 nên làm trị riêng 2 chỉ cho 1 hướng. Dạng Jordan của C chứa khối cỡ 2 ứng với trị riêng 2.

Lưu ý: số 1 nối hai cột có trị riêng khác nhau (ví dụ ô (2,3) của ma trận `[[2,1,0],[0,2,1],[0,0,3]]`) không tạo khối Jordan. Quan trọng là số 1 nằm trong nhóm cột cùng trị riêng.

## 6. Code kiểm tra và vẽ hình

Cần `numpy` và `matplotlib`:

```
pip install numpy matplotlib
```

Lưu thành `plot_diagonalization.py` rồi chạy `python plot_diagonalization.py`. Chương trình in kết quả kiểm tra và tạo hai ảnh `example1.png`, `example2.png`.

```python
import numpy as np
import matplotlib

matplotlib.use("Agg")
import matplotlib.pyplot as plt


def distinct_eigenvalues(M):
    vals = np.linalg.eigvals(M).real
    return sorted(set(np.round(vals, 6)))


def report(name, M):
    """In trị riêng, số hướng riêng và phép thử tích (A - lambda I)."""
    n = M.shape[0]
    I = np.eye(n)
    all_vals = np.linalg.eigvals(M).real
    P = I.copy()
    print(f"=== {name} ===")
    print(M)
    for lam in distinct_eigenvalues(M):
        times = int(np.sum(np.isclose(all_vals, lam, atol=1e-5)))
        n_dirs = n - np.linalg.matrix_rank(M - lam * I)
        print(f"lambda = {lam:g}: xuat hien {times} lan, co {n_dirs} huong rieng")
        P = P @ (M - lam * I)
    print("Tich cac (A - lambda I) theo tung tri rieng khac nhau:")
    print(np.round(P, 6))
    ok = np.allclose(P, 0)
    print("=> cheo hoa duoc" if ok else "=> KHONG cheo hoa duoc")
    print()


def draw_arrows(ax, vectors, labels, colors, title):
    for v, lab, c in zip(vectors, labels, colors):
        ax.annotate(
            "",
            xy=v,
            xytext=(0, 0),
            arrowprops=dict(arrowstyle="->", color=c, lw=2),
        )
        ax.text(v[0] + 0.08, v[1] + 0.08, lab, color=c, fontsize=11)
    ax.axhline(0, color="gray", lw=0.5)
    ax.axvline(0, color="gray", lw=0.5)
    ax.set_xlim(-0.5, 3)
    ax.set_ylim(-0.5, 3)
    ax.set_aspect("equal")
    ax.set_title(title)


def plot_example(M, name, filename):
    """Ve e1, e2 truoc va sau khi nhan M."""
    e1 = np.array([1.0, 0.0])
    e2 = np.array([0.0, 1.0])
    m1, m2 = M @ e1, M @ e2

    blue, green, red = "#378ADD", "#1D9E75", "#E24B4A"
    fig, (a, b) = plt.subplots(1, 2, figsize=(8, 4))

    draw_arrows(a, [e1, e2], ["e1", "e2"], [blue, green], "Truoc khi nhan")

    # e2 bi nghieng (khong cung huong voi e2) thi ve mau do va net dut huong cu
    tilted = not np.isclose(m2[0] * e2[1] - m2[1] * e2[0], 0)
    if tilted:
        b.plot([0, 0], [0, 2], "--", color="gray", lw=1)
    draw_arrows(
        b,
        [m1, m2],
        [f"{name}*e1", f"{name}*e2"],
        [blue, red if tilted else green],
        f"Sau khi nhan {name}",
    )

    fig.tight_layout()
    fig.savefig(filename, dpi=150, bbox_inches="tight")
    plt.close(fig)
    print(f"Da luu {filename}")


if __name__ == "__main__":
    A = np.array([[2, 0], [0, 2]], dtype=float)
    B = np.array([[2, 1], [0, 2]], dtype=float)
    C = np.array([[2, 1, 0], [0, 2, 0], [0, 0, 3]], dtype=float)

    report("Vi du 1: A", A)
    report("Vi du 2: B", B)
    report("Bai 3x3: C", C)

    plot_example(A, "A", "example1.png")
    plot_example(B, "B", "example2.png")
```

Kết quả mong đợi khi chạy:

- A: `lambda = 2` xuất hiện 2 lần, có 2 hướng riêng, tích bằng 0, chéo hóa được.
- B: `lambda = 2` xuất hiện 2 lần, chỉ có 1 hướng riêng, tích khác 0, không chéo hóa được.
- C: trị riêng 2 (2 lần, 1 hướng) và 3 (1 lần, 1 hướng), tích khác 0, không chéo hóa được.
