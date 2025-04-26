# Mood Journal: A Professional Tkinter App

This small Python app is a **Mood Journal**—a simple, elegant GUI for users to log their daily mood and a short note. It uses professional colors, frames, and fonts for a polished look.

---

### Features

- Modern color palette (soft blues/greys with accent)
- Custom fonts for headers and inputs
- Framed layout with clear separation of sections
- Input fields for date, mood (dropdown), and notes
- Save button that logs entries to a local file (`mood_journal.txt`)
- Confirmation message after saving

---

### Code

```python
import tkinter as tk
from tkinter import ttk, messagebox
from datetime import date

# Professional color palette & fonts
BG_COLOR = "#f4f6fb"
FRAME_COLOR = "#e3e7ef"
ACCENT_COLOR = "#5c7aea"
FONT_HEADER = ("Segoe UI", 16, "bold")
FONT_LABEL = ("Segoe UI", 11)
FONT_ENTRY = ("Segoe UI", 11)

def save_entry():
    entry_date = date_var.get()
    mood = mood_var.get()
    notes = notes_text.get("1.0", tk.END).strip()

    if not entry_date or not mood:
        messagebox.showwarning("Missing Info", "Please fill in all fields.")
        return
    
    with open("mood_journal.txt", "a") as f:
        f.write(f"{entry_date} | {mood} | {notes}\n")
    
    messagebox.showinfo("Saved!", "Your entry has been saved.")
    notes_text.delete("1.0", tk.END)

root = tk.Tk()
root.title("Mood Journal")
root.configure(bg=BG_COLOR)
root.geometry('400x350')
root.resizable(False, False)

main_frame = tk.Frame(root, bg=FRAME_COLOR, bd=2, relief=tk.RIDGE)
main_frame.place(relx=0.5, rely=0.5, anchor=tk.CENTER, width=340, height=290)

header_label = tk.Label(main_frame,
                        text="Mood Journal",
                        font=FONT_HEADER,
                        fg=ACCENT_COLOR,
                        bg=FRAME_COLOR)
header_label.pack(pady=(18,8))

# Date Entry (auto-filled but editable)
date_var = tk.StringVar(value=date.today().isoformat())
date_label = tk.Label(main_frame,
                      text="Date:",
                      font=FONT_LABEL,
                      bg=FRAME_COLOR)
date_label.pack(anchor='w', padx=(24), pady=(6))
date_entry = ttk.Entry(main_frame,
                       textvariable=date_var,
                       font=FONT_ENTRY,
                       width=15)
date_entry.pack(anchor='w', padx=(24))

# Mood Dropdown
mood_var = tk.StringVar()
mood_label = tk.Label(main_frame,
                      text="Mood:",
                      font=FONT_LABEL,
                      bg=FRAME_COLOR)
mood_label.pack(anchor='w', padx=(24), pady=(10))
moods_list=["😊 Happy","😐 Neutral","😔 Sad","😠 Angry","😰 Anxious"]
mood_comboBox=tk.ttk.Combobox(main_frame,textvariable=mood_var,font=("Segoe UI",11),
                              values=moods_list,state="readonly")
mood_comboBox.set("")
mood_comboBox.pack(anchor='w',padx=(24))

# Notes Text Field
notes_label=tk.Label(main_frame,text="Notes:",font=FONT_LABEL,bg=FRAME_COLOR)
notes_label.pack(anchor='w',padx=(24),pady=(10))
notes_text=tk.Text(main_frame,height=3,width=28,font=("Segoe UI",10))
notes_text.pack(padx=(20))

save_btn=tk.Button(
    main_frame,text="Save Entry",
    command=lambda: save_entry(),
    bg="#4254d2",
    fg="#fff",
    activebackground="#32409c",
    activeforeground="#fff",
    relief=tk.FLAT,font=("Segoe UI Semibold",12),
   cursor="hand2"
 )
save_btn.pack(pady=(14))

root.mainloop()
```

---

## README.md

> ### Mood Journal – Tkinter Desktop App  
>
> **What it does:**  
> The Mood Journal lets you quickly log your daily emotional state along with an optional note in an attractive desktop interface.
>
> **How it works:**  
> - When you launch the app (`python mood_journal.py`), you'll see fields for the current date (editable), your selected *Mood* from a dropdown menu of emojis/descriptions ("Happy", "Neutral", etc.), and a space to write any thoughts or context.
> - Click "Save Entry" to record your input; each submission is appended as one line in `mood_journal.txt` in the same folder.
>
> **Design choices:**  
> - Uses modern blue/grey tones and Segoe UI fonts for clarity and professionalism.
> - All elements are grouped within a framed area centered on the window.
>
> **Requirements:**  
> - Python 3.x (Tkinter comes pre-installed).
>
> ---
>
> Enjoy tracking your moods!

---

This example demonstrates how to use frames, custom colors/fonts, labels/entries/buttons, themed widgets (`ttk.Combobox`), event handling, file I/O—all wrapped into an elegant mini-app suitable even as a template for more advanced journaling tools.