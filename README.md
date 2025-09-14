# 🎮 Sword Game

## 📌 รายละเอียดโปรเจกต์
**Sword Game** เป็นเกม 2D ที่สร้างด้วย **Unity** โดยมีระบบ **Animation** และ **Gameplay** พื้นฐาน  
ตัวละครสามารถทำ Action ได้หลายแบบ เช่น วิ่ง กระโดด บาดเจ็บ และตาย พร้อมระบบ **UI Restart**  

---

## 🚀 ฟีเจอร์หลัก
- ระบบควบคุมตัวละคร:
  - Idle (ยืน)
  - Run (เดิน/วิ่ง)
  - Jump (กระโดด)
  - Hurt (บาดเจ็บ)
  - Dead (ตาย)
- ระบบ UI Restart
- เอฟเฟกต์กราฟิกด้วย ShaderLab + HLSL
- จัดการ State การเคลื่อนไหวผ่าน Unity Animator

---

## 🛠 เทคโนโลยีที่ใช้
- **Unity Engine** (2D)
- **C#**
- **ShaderLab / HLSL**
- **Unity Animator**

---

## 📂 โครงสร้างไฟล์
SwordGAem-main-2/
│
├── Assets/
│ ├── Scripts/ # โค้ด C# ควบคุมเกม
│ ├── Animations/ # Animation Controller
│ ├── Sprites/ # Sprite ตัวละคร (Idle, Jump, Run, Hurt, Dead)
│ └── UI/ # UI เช่น ปุ่ม Restart
│
├── ProjectSettings/
├── Packages/
├── README.md
└── .gitignore

csharp
คัดลอกโค้ด

---

## 🎮 วิธีการเล่น
1. เปิดโปรเจกต์ด้วย **Unity (แนะนำ 2021 ขึ้นไป)**  
2. กด **Play** เพื่อเริ่มเกม  
3. ควบคุมตัวละครด้วยคีย์บอร์ด:  
   - **← / →** : เดินซ้าย-ขวา  
   - **Spacebar** : กระโดด  
4. เมื่อแพ้ สามารถกด **Restart** เพื่อเริ่มเกมใหม่  

---

## 📜 โค้ดตัวอย่าง

### 🔹 Script ควบคุมการกระโดด
```csharp
using UnityEngine;

public class PlayerController : MonoBehaviour
{
    public float speed = 5f;
    public float jumpForce = 5f;
    public Rigidbody2D rb;
    private bool grounded = false;

    void Update()
    {
        float move = Input.GetAxis("Horizontal");
        rb.velocity = new Vector2(move * speed, rb.velocity.y);

        if (Input.GetKeyDown(KeyCode.Space) && grounded)
        {
            rb.velocity = new Vector2(rb.velocity.x, jumpForce);
        }
    }

    void OnCollisionEnter2D(Collision2D collision)
    {
        if (collision.gameObject.CompareTag("Ground"))
        {
            grounded = true;
        }
    }

    void OnCollisionExit2D(Collision2D collision)
    {
        if (collision.gameObject.CompareTag("Ground"))
        {
            grounded = false;
        }
    }
}
🔹 Script จัดการสถานะอนิเมชัน
csharp
คัดลอกโค้ด
using UnityEngine;

public class PlayerAnimation : MonoBehaviour
{
    public Animator animator;
    private Rigidbody2D rb;

    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    void Update()
    {
        animator.SetFloat("Speed", Mathf.Abs(rb.velocity.x));
        animator.SetBool("IsJumping", rb.velocity.y > 0.1f);
        animator.SetBool("IsFalling", rb.velocity.y < -0.1f);
    }

    public void Hurt()
    {
        animator.SetTrigger("Hurt");
    }

    public void Dead()
    {
        animator.SetTrigger("Dead");
    }
}
📸 ตัวอย่างภาพ
(สามารถใส่ภาพจาก Assets/Sprites ได้ เช่น Idle.png, Run.png, Jump.png)

markdown
คัดลอกโค้ด
![Idle](Assets/Sprites/Idle.png)
![Run](Assets/Sprites/Run.png)
![Jump](Assets/Sprites/Jump.png)
![idle](https://github.com/user-attachments/assets/fab89433-84d4-44c9-9ee8-6c524b52659a)
กระโดด
![jump](https://github.com/user-attachments/assets/1a5b77cb-2b43-469b-a909-995163d5be48)
เดินหน้า และกลับหลัง
![Run](https://github.com/user-attachments/assets/443c8442-c6ec-48f8-a4cd-2b6f21e173c9)
บาดเจ็บ
![Hurt](https://github.com/user-attachments/assets/28c34f09-0d84-44cc-aacf-17a9feca2adb)
ตาย (หยุดการเคลื่อนไหว)
![Dead](https://github.com/user-attachments/assets/2856189a-34d9-45bb-acbc-fc10e7158a74)

![UIRestart9-ezgif com-optimize](https://github.com/user-attachments/assets/2a229b84-15f6-4579-b3e2-a4eae12cdee9)
