# Stick-Diagram
This project is a Python-based tool designed to convert a Boolean expression into a Stick Diagram.
### **Quy tắc xác định các cạnh (Edges) trong mạng NMOS**

#### **1. Các thành phần cơ bản của mạng NMOS**
- **Source (S):** Điểm nối với đất (GND) hoặc với transistor khác.
- **Drain (D):** Điểm nối với đầu ra hoặc với transistor khác.
- **Transistor:** Mỗi biến trong biểu thức Boolean (ví dụ: A, B, C...) được biểu diễn bằng một transistor với một source (S) và một drain (D).

#### **2. Quy tắc xác định các cạnh**
Dựa trên biểu thức Boolean, các cạnh trong đồ thị được xác định như sau:

1. **Kết nối nối tiếp (`*`):**
   - Khi hai biến được nối với nhau qua phép `*` (AND), các transistor tương ứng sẽ được nối nối tiếp.
   - **Cách kết nối:**
     - Drain (D) của transistor trước nối với Source (S) của transistor sau.
   - **Ví dụ:**
     - Với `A*B`, các cạnh sẽ là:
       ```
       (AS, AD)   # Source của A nối với đất (GND)
       (AD, BS)   # Drain của A nối với Source của B
       (BD, DD)   # Drain của B nối với đầu ra
       ```

2. **Kết nối song song (`+`):**
   - Khi hai biến được nối với nhau qua phép `+` (OR), các transistor tương ứng sẽ được nối song song.
   - **Cách kết nối:**
     - Source (S) của cả hai transistor được nối chung.
     - Drain (D) của cả hai transistor được nối chung.
   - **Ví dụ:**
     - Với `A+B`, các cạnh sẽ là:
       ```
       (AS, BS)   # Source của A và B nối chung
       (AD, BD)   # Drain của A và B nối chung
       ```

3. **Biến đơn lẻ:**
   - Nếu một biến xuất hiện mà không có phép toán `*` hoặc `+`, nó được kết nối độc lập.
   - **Cách kết nối:**
     - Source (S) nối với đất (GND).
     - Drain (D) nối với đầu ra.
   - **Ví dụ:**
     - Với `E`, các cạnh sẽ là:
       ```
       (ES, ED)   # Source của E nối với GND, Drain nối với đầu ra
       ```

---

### **Chu trình tìm đường đi Euler Path**

#### **1. Định nghĩa Euler Path**
- Euler Path là một đường đi trong đồ thị mà mỗi cạnh được đi qua đúng **một lần duy nhất**.
- Đối với mạng NMOS, Euler Path được sử dụng để tối ưu hóa việc kết nối các transistor sao cho tất cả các cạnh được sắp xếp hợp lý.

#### **2. Điều kiện tồn tại Euler Path**
- Euler Path tồn tại trong đồ thị nếu:
  1. Đồ thị liên thông.
  2. Số đỉnh có bậc lẻ trong đồ thị là **0 hoặc 2**.

#### **3. Quy trình tìm Euler Path**
1. **Xây dựng đồ thị:**
   - Sử dụng các **nodes (đỉnh)** và **edges (cạnh)** theo quy tắc xác định cạnh ở trên.

2. **Kiểm tra điều kiện Euler Path:**
   - Kiểm tra số lượng đỉnh có bậc lẻ:
     - Nếu số đỉnh có bậc lẻ là 0 → Tồn tại chu trình Euler (Euler Circuit).
     - Nếu số đỉnh có bậc lẻ là 2 → Tồn tại đường đi Euler (Euler Path).
     - Nếu số đỉnh có bậc lẻ khác 0 hoặc 2 → Không tồn tại đường đi Euler.

3. **Tìm đường đi:**
   - Bắt đầu từ một đỉnh có bậc lẻ (nếu tồn tại) hoặc từ bất kỳ đỉnh nào (nếu không có đỉnh lẻ).
   - Đi qua từng cạnh đúng một lần, sử dụng thuật toán DFS (Depth First Search) hoặc thuật toán Fleury.

4. **Kết quả:**
   - Trả về danh sách các đỉnh (nodes) theo thứ tự đường đi Euler Path.

#### **4. Ví dụ minh họa**
- Với biểu thức Boolean `A*B + E + C*D`, đồ thị có các cạnh:
  ```
  [('AS', 'AD'), ('AD', 'BS'), ('BS', 'BD'), 
   ('ES', 'ED'), 
   ('CS', 'CD'), ('CD', 'DS'), ('DS', 'DD'),
   ('AS', 'ES'), ('AS', 'CS'), ('ES', 'CS'),
   ('AD', 'ED'), ('BD', 'ED'), ('CD', 'ED')]
  ```
- Một **Euler Path** có thể là:
  ```
  ['AS', 'AD', 'BS', 'BD', 'ES', 'ED', 'CS', 'CD', 'DS', 'DD']
  ```
### **Quy tắc xác định các cạnh (Edges) trong mạng PMOS**

#### **1. Các thành phần cơ bản của mạng PMOS**
- **Source (S):** Điểm nối với VCC (nguồn cao) hoặc với transistor khác.
- **Drain (D):** Điểm nối với đầu ra hoặc với transistor khác.
- **Transistor:** Mỗi biến trong biểu thức Boolean (ví dụ: A, B, C, E...) được biểu diễn bằng một transistor với một source (S) và một drain (D).

#### **2. Quy tắc xác định các cạnh**
Dựa trên biểu thức Boolean, các cạnh trong đồ thị được xác định như sau:

1. **Kết nối song song (`+`):**
   - Khi hai biến được nối với nhau qua phép `+` (OR), các transistor tương ứng sẽ được nối song song.
   - **Cách kết nối:**
     - Source (S) của cả hai transistor được nối chung.
     - Drain (D) của cả hai transistor được nối chung.
   - **Ví dụ:**
     - Với `A+B`, các cạnh sẽ là:
       ```
       (AS, BS)   # Source của A và B nối chung
       (AD, BD)   # Drain của A và B nối chung
       ```

2. **Kết nối nối tiếp (`*`):**
   - Khi hai biến được nối với nhau qua phép `*` (AND), các transistor tương ứng sẽ được nối nối tiếp.
   - **Cách kết nối:**
     - Drain (D) của transistor trước nối với Source (S) của transistor sau.
   - **Ví dụ:**
     - Với `A*B`, các cạnh sẽ là:
       ```
       (AS, AD)   # Source của A nối với VCC
       (AD, BS)   # Drain của A nối với Source của B
       (BD, DD)   # Drain của B nối với đầu ra
       ```

3. **Biến đơn lẻ:**
   - Nếu một biến xuất hiện mà không có phép toán `*` hoặc `+`, nó được kết nối độc lập.
   - **Cách kết nối:**
     - Source (S) nối với VCC.
     - Drain (D) nối với đầu ra.
   - **Ví dụ:**
     - Với `E`, các cạnh sẽ là:
       ```
       (ES, ED)   # Source của E nối với VCC, Drain nối với đầu ra
       ```

#### **4. Đặc điểm mạng PMOS:**
- PMOS được thiết kế để kéo điện thế lên cao (pull-up).
- Vì vậy, các transistor PMOS có source (S) kết nối với nguồn cao (VCC) và drain (D) kết nối với đầu ra.

---

### **Chu trình tìm đường đi Euler Path trong PMOS**

#### **1. Định nghĩa Euler Path**
- Euler Path trong mạng PMOS là đường đi qua tất cả các cạnh đúng **một lần duy nhất**.
- Đường đi này cần tuân theo cách các transistor được kết nối, sao cho tất cả các cạnh của đồ thị được sử dụng.

#### **2. Điều kiện tồn tại Euler Path**
- Euler Path tồn tại trong đồ thị nếu:
  1. Đồ thị liên thông.
  2. Số đỉnh có bậc lẻ trong đồ thị là **0 hoặc 2**.

#### **3. Quy trình tìm Euler Path**
1. **Xây dựng đồ thị:**
   - Sử dụng các **nodes (đỉnh)** và **edges (cạnh)** theo quy tắc xác định cạnh ở trên.

2. **Đảo ngược biểu thức Boolean:**
   - Để tạo mạng PMOS, biểu thức Boolean cần được đảo ngược:
     - `+` (OR) → `*` (AND).
     - `*` (AND) → `+` (OR).
   - **Ví dụ:**
     - Biểu thức gốc: `A*B + E + C*D`.
     - Biểu thức đảo ngược: `(A+B)*E*(C+D)`.

3. **Kiểm tra điều kiện Euler Path:**
   - Kiểm tra số lượng đỉnh có bậc lẻ:
     - Nếu số đỉnh có bậc lẻ là 0 → Tồn tại chu trình Euler (Euler Circuit).
     - Nếu số đỉnh có bậc lẻ là 2 → Tồn tại đường đi Euler (Euler Path).
     - Nếu số đỉnh có bậc lẻ khác 0 hoặc 2 → Không tồn tại đường đi Euler.

4. **Tìm đường đi:**
   - Bắt đầu từ một đỉnh có bậc lẻ (nếu tồn tại) hoặc từ bất kỳ đỉnh nào (nếu không có đỉnh lẻ).
   - Đi qua từng cạnh đúng một lần, sử dụng thuật toán DFS (Depth First Search) hoặc thuật toán Fleury.

5. **Kết quả:**
   - Trả về danh sách các đỉnh (nodes) theo thứ tự đường đi Euler Path.

---

### **Ví dụ minh họa**

#### **Biểu thức Boolean gốc: `A*B + E + C*D`**
1. **Đảo ngược biểu thức Boolean:**
   - `(A+B)*E*(C+D)`.

2. **Phân tích cách kết nối:**
   - `A+B`: A và B nối song song.
   - `C+D`: C và D nối song song.
   - `(A+B)*E*(C+D)`: Các nhóm `(A+B)` và `(C+D)` được nối nối tiếp với E.

3. **Xác định các cạnh trong mạng PMOS:**
   ```
   [('AS', 'BS'), ('AD', 'BD'),   # A và B song song
    ('CS', 'DS'), ('CD', 'DD'),   # C và D song song
    ('ES', 'ED'),                 # E độc lập
    ('BS', 'ES'), ('BD', 'ED'),   # Nhóm A+B nối với E
    ('DS', 'ES'), ('DD', 'ED')]   # Nhóm C+D nối với E
   ```

4. **Tìm Euler Path:**
   - Một **Euler Path** có thể là:
     ```
     ['AS', 'BS', 'ES', 'ED', 'BD', 'AD', 'CS', 'DS', 'DD', 'CD']
     ```

---

### **Tóm tắt**
- **Cách xác định cạnh (Edges):**
  - Kết nối song song (`+`) và nối tiếp (`*`) được xử lý dựa trên biểu thức Boolean.
  - Đảo ngược biểu thức Boolean để phù hợp với mạng PMOS.
- **Tìm Euler Path:**
  - Xây dựng đồ thị từ các cạnh của PMOS.
  - Sử dụng thuật toán để tìm đường đi Euler Path.
- **Ví dụ minh họa:**
  - Biểu thức `A*B + E + C*D` được chuyển đổi và xử lý để tạo đồ thị PMOS và đường đi Euler Path.
### **nối nguồn và đất trong CMOS**

#### **1. Nối nguồn đất và đầu ra trong NMOS (Pull-Down Network)**

##### **Nguyên tắc kết nối NMOS**
- **Source (S):** Mỗi transistor trong NMOS phải có **source nối với đất (GND)** hoặc với drain của transistor trước đó (trong trường hợp nối tiếp).
- **Drain (D):** Drain của các transistor cuối cùng trong mạng NMOS được nối với đầu ra (OUT).
- **Mục tiêu của NMOS:** Kéo đầu ra xuống mức điện áp thấp (GND) khi biểu thức logic yêu cầu.

##### **Cách nối:**
1. **Source nối với đất (GND):**
   - Tất cả các transistor đầu tiên trong mạng (ở nhánh hoặc nhóm đầu tiên) phải có **source nối trực tiếp với GND**.

2. **Drain của transistor cuối nối với OUT:**
   - Tất cả các transistor cuối cùng của mạng (ở nhánh cuối cùng) phải có **drain nối với đầu ra OUT**.

3. **Kết nối nối tiếp (`*`):**
   - Drain (D) của transistor trước nối với Source (S) của transistor sau.
   - Ví dụ: Với biểu thức `A*B`, A và B được nối nối tiếp:
     ```
     Source của A nối với GND → (AS, AD)
     Drain của A nối với Source của B → (AD, BS)
     Drain của B nối với OUT → (BD, OUT)
     ```

4. **Kết nối song song (`+`):**
   - Source (S) của các transistor trong nhánh song song được nối chung với đất (GND).
   - Drain (D) của các transistor trong nhánh song song được nối chung với OUT.
   - Ví dụ: Với biểu thức `A+B`, A và B được nối song song:
     ```
     Source của A và B nối với GND → (AS, BS)
     Drain của A và B nối với OUT → (AD, BD)
     ```

##### **Ví dụ minh họa:**
Biểu thức `A*B + C*D`:
- `A*B`: A và B nối nối tiếp.
  ```
  Source của A nối với GND → (AS, AD)
  Drain của A nối với Source của B → (AD, BS)
  Drain của B nối với OUT → (BD, OUT)
  ```
- `C*D`: C và D nối nối tiếp.
  ```
  Source của C nối với GND → (CS, CD)
  Drain của C nối với Source của D → (CD, DS)
  Drain của D nối với OUT → (DD, OUT)
  ```
- Kết nối song song giữa `A*B` và `C*D`:
  ```
  Source của A và C nối với GND → (AS, CS)
  Drain của B và D nối với OUT → (BD, DD)
  ```

---

#### **2. Nối nguồn và đầu ra trong PMOS (Pull-Up Network)**

##### **Nguyên tắc kết nối PMOS**
- **Source (S):** Mỗi transistor trong PMOS phải có **source nối với nguồn cao (VCC)** hoặc với drain của transistor trước đó (trong trường hợp nối tiếp).
- **Drain (D):** Drain của các transistor cuối cùng trong mạng PMOS được nối với đầu ra (OUT).
- **Mục tiêu của PMOS:** Kéo đầu ra lên mức điện áp cao (VCC) khi biểu thức logic yêu cầu.

##### **Cách nối:**
1. **Source nối với VCC:**
   - Tất cả các transistor đầu tiên trong mạng (ở nhánh hoặc nhóm đầu tiên) phải có **source nối trực tiếp với VCC**.

2. **Drain của transistor cuối nối với OUT:**
   - Tất cả các transistor cuối cùng của mạng (ở nhánh cuối cùng) phải có **drain nối với đầu ra OUT**.

3. **Kết nối nối tiếp (`*`):**
   - Drain (D) của transistor trước nối với Source (S) của transistor sau.
   - Ví dụ: Với biểu thức `(A+B)*C`, sau khi đảo biểu thức thành `A*B + C`:
     ```
     Source của A nối với VCC → (AS, AD)
     Drain của A nối với Source của B → (AD, BS)
     Source của C nối với VCC → (CS, CD)
     Drain của B nối với OUT → (BD, OUT)
     Drain của C nối với OUT → (CD, OUT)
     ```

4. **Kết nối song song (`+`):**
   - Source (S) của các transistor trong nhánh song song được nối chung với VCC.
   - Drain (D) của các transistor trong nhánh song song được nối chung với OUT.
   - Ví dụ: Với biểu thức `A+B`, A và B được nối song song:
     ```
     Source của A và B nối với VCC → (AS, BS)
     Drain của A và B nối với OUT → (AD, BD)
     ```

##### **Ví dụ minh họa:**
Biểu thức `(A+B)*C`:
- `A+B`: A và B nối song song.
  ```
  Source của A và B nối với VCC → (AS, BS)
  Drain của A và B nối với Source của C → (AD, BD nối với CS)
  ```
- `C`: C nối nối tiếp với nhóm `A+B`.
  ```
  Source của C nối với VCC → (CS, CD)
  Drain của C nối với OUT → (CD, OUT)
  ```

---

#### **3. So sánh giữa NMOS và PMOS**

| Thành phần             | NMOS (Pull-Down Network)             | PMOS (Pull-Up Network)              |
|-----------------------|-------------------------------------|-------------------------------------|
| **Source (S)**        | Nối với đất (GND)                  | Nối với nguồn cao (VCC)            |
| **Drain (D)**         | Nối với đầu ra (OUT)               | Nối với đầu ra (OUT)               |
| **Mục tiêu**          | Kéo điện áp xuống thấp (GND)       | Kéo điện áp lên cao (VCC)          |
| **Kết nối nối tiếp**  | Drain (D) nối với Source (S)       | Drain (D) nối với Source (S)       |
| **Kết nối song song** | Source (S) nối chung với GND       | Source (S) nối chung với VCC       |

---

#### **4. Tóm tắt**
- **NMOS:**
  - Source nối với GND.
  - Drain của transistor cuối nối với OUT.
  - Hoạt động để kéo đầu ra xuống mức thấp (GND).

- **PMOS:**
  - Source nối với VCC.
  - Drain của transistor cuối nối với OUT.
  - Hoạt động để kéo đầu ra lên mức cao (VCC).
