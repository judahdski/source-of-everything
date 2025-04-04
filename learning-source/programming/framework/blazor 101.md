### **1️⃣ Apa itu Blazor?**

Blazor adalah **framework UI** untuk membangun aplikasi web interaktif dengan menggunakan **C#** dan **.NET**. Blazor memungkinkan developer untuk menulis aplikasi **single-page application (SPA)** menggunakan C# di sisi client, bukan JavaScript.

Blazor memiliki dua model aplikasi utama:

-   **Blazor Server**: Aplikasi dijalankan di server, UI diperbarui melalui SignalR.
-   **Blazor WebAssembly**: Aplikasi dijalankan langsung di browser dengan WebAssembly.

### **2️⃣ Komponen Blazor**

-   Blazor menggunakan **komponen** sebagai unit UI. Komponen adalah **file `.razor`** yang berisi HTML dan C# di dalamnya.
-   **Stateful Components**: Komponen yang memiliki state lokal, seperti nilai variabel atau properti, dan dapat diupdate saat pengguna berinteraksi dengan UI.

#### **Contoh Komponen:**

```razor
@code {
    private string Name = "Blazor";
}

<h3>Hello, @Name!</h3>
```

-   **`@code`** digunakan untuk menulis **C# code** di dalam file `.razor`.

---

### **3️⃣ Razor Syntax dan Templating**

**Razor** adalah engine templating untuk **Blazor** dan **ASP.NET Core**. Razor memungkinkan kita menulis **markup HTML dan C#** bersama-sama dalam file `.razor` atau `.cshtml`.

-   **`@` digunakan untuk menulis C# di dalam HTML**.
-   **Looping & Kondisional**: Blazor mendukung penggunaan **`@foreach`**, **`@if`**, dan lainnya.

#### **Contoh Kondisional dan Looping:**

```razor
@foreach (var item in items)
{
    <li>@item</li>
}

@if (items.Count == 0)
{
    <p>No items found.</p>
}
```

### **4️⃣ Data Binding di Blazor**

**Data binding** adalah teknik untuk **menghubungkan data model** dengan UI. Blazor mendukung beberapa jenis data binding.

#### **One-Way Data Binding**:

-   Data mengalir dari model ke UI.

```razor
<h3>Counter: @counter</h3>

@code {
    private int counter = 0;
}
```

#### **Two-Way Data Binding**:

-   Data dapat mengalir dua arah antara model dan UI.

```razor
<input @bind="userName" />
<h3>Nama: @userName</h3>

@code {
    private string userName = "Blazor Dev";
}
```

#### **Event Binding**:

Blazor juga memungkinkan kita menangani event, seperti `@onclick`, `@oninput`, dll.

```razor
<button @onclick="IncrementCounter">Tambah</button>

@code {
    private int counter = 0;
    private void IncrementCounter() => counter++;
}
```

---

### **5️⃣ State Management di Blazor**

**State management** adalah bagaimana kita **menyimpan dan mengelola data** selama aplikasi berjalan.

-   **Blazor Server**: State disimpan di server. Jika koneksi terputus, state hilang.
-   **Blazor WebAssembly**: State disimpan di browser, tetapi hilang setelah refresh.

#### **Metode Penyimpanan State:**

1. **Component State** (variabel biasa): Hanya berlaku di komponen.
2. **Scoped Services**: Menggunakan **dependency injection** untuk menyimpan state selama sesi.
3. **Local Storage**: Menyimpan state secara permanen di browser (setelah refresh).
4. **Session Storage**: Menyimpan state selama sesi per browser.
5. **Protected Browser Storage**: Menyimpan data secara aman di Blazor Server.

```razor
@inject ILocalStorageService localStorage

<h3>Counter: @counter</h3>
<button @onclick="IncrementCounter">Tambah</button>

@code {
    private int counter = 0;

    protected override async Task OnInitializedAsync()
    {
        counter = await localStorage.GetItemAsync<int>("counter");
    }

    private async Task IncrementCounter()
    {
        counter++;
        await localStorage.SetItemAsync("counter", counter);
    }
}
```

---

### **6️⃣ Event Handling di Blazor**

**Event handling** memungkinkan kita merespon aksi pengguna seperti klik, input, dll.

-   **Event Handler**: Menghubungkan event UI (misalnya `@onclick`) dengan method C#.
-   **Passing Parameters to Events**: Kita bisa mengirimkan parameter ke event handler.

#### **Contoh Event Handling**:

```razor
<button @onclick="IncrementCounter">Tambah</button>
<p>Counter: @counter</p>

@code {
    private int counter = 0;

    private void IncrementCounter() => counter++;
}
```

#### **Passing Parameters to Events**:

```razor
<button @onclick="() => IncrementByAmount(5)">Tambah 5</button>

@code {
    private int counter = 0;

    private void IncrementByAmount(int amount)
    {
        counter += amount;
    }
}
```

---

### **7️⃣ Blazor Lifecycle**

Blazor memiliki **lifecycle methods** yang memberikan kontrol atas **siklus hidup komponen**. Beberapa method lifecycle yang penting adalah:

-   **`OnInitialized`**: Dipanggil saat komponen pertama kali diinisialisasi.
-   **`OnParametersSet`**: Dipanggil setiap kali parameter komponen berubah.
-   **`OnAfterRender`**: Dipanggil setelah render pertama selesai.

```razor
@code {
    protected override void OnInitialized()
    {
        // Initialization code
    }

    protected override void OnAfterRender(bool firstRender)
    {
        if (firstRender)
        {
            // Do something only on the first render
        }
    }
}
```

---

### **8️⃣ Routing di Blazor**

Blazor memiliki **routing system** yang memungkinkan kita mendefinisikan URL dan memetakan ke komponen.

-   **`@page`**: Mendefinisikan URL yang dipetakan ke komponen.

#### **Contoh Routing**:

```razor
@page "/counter"

<h3>Counter: @counter</h3>
<button @onclick="IncrementCounter">Tambah</button>

@code {
    private int counter = 0;

    private void IncrementCounter() => counter++;
}
```

-   **Multiple Routes**: Satu komponen bisa menangani beberapa route.

```razor
@page "/counter/{id:int}"

<h3>Counter ID: @id</h3>

@code {
    [Parameter] public int id { get; set; }
}
```

---

### **9️⃣ Dependency Injection di Blazor**

Blazor menggunakan **Dependency Injection (DI)** untuk mengelola servis dan menyediakan instansi di seluruh komponen.

-   **`AddSingleton<T>()`**: Menggunakan satu instansi sepanjang aplikasi.
-   **`AddScoped<T>()`**: Menggunakan instansi yang berbeda per sesi user.
-   **`AddTransient<T>()`**: Menggunakan instansi baru setiap kali dibutuhkan.

#### **Contoh Dependency Injection**:

```razor
@inject IMyService myService

<h3>Data: @myService.GetData()</h3>

@code {
    public interface IMyService
    {
        string GetData();
    }

    public class MyService : IMyService
    {
        public string GetData() => "Hello from MyService!";
    }
}
```

---

### **10. Komunikasi Antar Komponen**

-   **Dari Parent ke Child:** Gunakan `[Parameter]`
-   **Dari Child ke Parent:** Gunakan **EventCallback**

**Parent ke Child:**

```razor
<CounterComponent StartValue="5" />
```

```razor
// CounterComponent.razor
<p>Hitungan: @count</p>

@code {
    [Parameter] public int StartValue { get; set; }
    private int count;

    protected override void OnInitialized()
    {
        count = StartValue;
    }
}
```

**Child ke Parent dengan `EventCallback`:**

```razor
// ChildComponent.razor
<button @onclick="SendData">Klik Saya</button>

@code {
    [Parameter] public EventCallback<string> OnButtonClick { get; set; }

    private async Task SendData()
    {
        await OnButtonClick.InvokeAsync("Data dari anak");
    }
}
```

**Di Parent Component:**

```razor
<ChildComponent OnButtonClick="HandleChildClick" />

@code {
    private void HandleChildClick(string message)
    {
        Console.WriteLine(message);
    }
}
```

---

### **11. Komponen Dinamis & RenderFragment**

Jika kamu ingin membuat komponen yang dapat menampilkan elemen secara dinamis, gunakan **RenderFragment**.

**Contoh komponen template:**

```razor
<DynamicContainer>
    <h3>Konten Dinamis</h3>
</DynamicContainer>
```

```razor
// DynamicContainer.razor
<div class="box">
    @ChildContent
</div>

@code {
    [Parameter] public RenderFragment ChildContent { get; set; }
}
```
---

### 🧠 **12. Form Component: `<EditForm>`**
Ini base-nya semua form. Kalau lo mau bikin form validasi proper, **selalu mulai dari sini**.

```razor
<EditForm Model="@user" OnValidSubmit="HandleValidSubmit">
    ...
</EditForm>
```

### Props penting:
- `Model` → object data binding
- `OnValidSubmit` → event saat form valid
- `OnInvalidSubmit` → event saat form gak valid

---

## 🧩 **Built-in Input Components**

### 🔤 `InputText`
```razor
<InputText @bind-Value="user.Name" class="form-control" />
```

### 🔢 `InputNumber<T>`
```razor
<InputNumber @bind-Value="user.Age" class="form-control" />
```

### ✅ `InputCheckbox`
```razor
<InputCheckbox @bind-Value="user.IsActive" />
```

### 📅 `InputDate<T>`
```razor
<InputDate @bind-Value="user.BirthDate" />
```

### 📎 `InputSelect<T>`
```razor
<InputSelect @bind-Value="user.Gender">
    <option value="">-- Select Gender --</option>
    <option>Male</option>
    <option>Female</option>
</InputSelect>
```

> Semua komponen ini otomatis ngerti validasi, selama lo pakai `EditForm`.

---

## 🛡️ **Validasi di Blazor**

### 1. **Gunakan Model + Data Annotations**
```csharp
public class UserModel {
    [Required]
    [StringLength(100)]
    public string Name { get; set; }

    [Range(18, 99)]
    public int Age { get; set; }

    [EmailAddress]
    public string Email { get; set; }
}
```

### 2. **Tambahkan Validator di Form**
```razor
<EditForm Model="@user" OnValidSubmit="Save">
    <DataAnnotationsValidator />
    <ValidationSummary />
    <InputText @bind-Value="user.Name" />
</EditForm>
```

---

## 🔁 **Binding & Two-Way Update**
Dengan `@bind-Value`, komponen input akan otomatis update model saat user isi form dan sebaliknya.

> Mirip kayak `v-model` di Vue atau `useState + onChange` di React tapi less headache.

---

## 🔧 **Custom Validation (Kalau Default Kurang Ganas)**
Lo bisa bikin custom validator dengan **`IValidator`** atau pakai **`FluentValidation`**. Tapi untuk kebanyakan use case, DataAnnotations udah cukup.

---

## ⚙️ **Form Events Penting**
- `OnSubmit` → Triggered setiap submit (valid atau tidak)
- `OnValidSubmit` → Hanya jalan kalau form valid
- `OnInvalidSubmit` → Hanya jalan kalau form gak valid

---

## 👀 **Tampilan Validasi Per Field**
```razor
<InputText @bind-Value="user.Email" />
<ValidationMessage For="@(() => user.Email)" />
```

> Ini akan munculin error spesifik untuk `Email` aja. Gak semua error ditumpuk di `ValidationSummary`.

---

### ✅ Contoh Komplet

```razor
<EditForm Model="@user" OnValidSubmit="HandleSubmit">
    <DataAnnotationsValidator />
    <ValidationSummary />

    <div>
        <label>Nama:</label>
        <InputText @bind-Value="user.Name" />
        <ValidationMessage For="@(() => user.Name)" />
    </div>

    <div>
        <label>Email:</label>
        <InputText @bind-Value="user.Email" />
        <ValidationMessage For="@(() => user.Email)" />
    </div>

    <button type="submit">Submit</button>
</EditForm>

@code {
    private UserModel user = new();

    private void HandleSubmit()
    {
        // Simpan ke DB atau apapun
        Console.WriteLine($"User: {user.Name}, Email: {user.Email}");
    }

    public class UserModel
    {
        [Required]
        public string Name { get; set; }

        [EmailAddress]
        public string Email { get; set; }
    }
}
```
---
### **12. Advanced Topics in Blazor**

Setelah memahami dasar-dasar Blazor, ada beberapa topik lanjutan yang perlu dipelajari:

#### **1. Performance Optimization**

-   **Lazy Loading**: Memuat komponen atau data hanya saat dibutuhkan.
-   **Virtualization**: Efisiensikan rendering daftar besar menggunakan **`<Virtualize>`**.

#### **2. WebAssembly Interop**

Menggunakan **JavaScript interop** di Blazor WASM untuk menggunakan fitur yang tidak tersedia di Blazor (seperti akses API browser).

#### **3. Blazor with Server-Side Rendering (SSR)**

Menggunakan **ASP.NET Core** untuk melakukan rendering sisi server dan mengirimkan HTML ke client, sangat cocok untuk aplikasi SEO-friendly.

#### **4. Authentication and Authorization**

Blazor mendukung integrasi **Identity** dan **OAuth** untuk mengelola autentikasi dan otorisasi user.

---