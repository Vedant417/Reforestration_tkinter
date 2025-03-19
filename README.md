# Reforestration_tkinter
from tkinter import *
from tkinter import ttk, messagebox
from PIL import ImageTk, Image
import os

def load_image(image_path):
    """Load and return an ImageTk.PhotoImage object."""
    if os.path.isfile(image_path):
        image = Image.open(image_path)
        return ImageTk.PhotoImage(image)
    else:
        print(f"Error: Image file '{image_path}' not found.")
        return None

def open_top_level(title):
    if title in ['To Plant Trees', 'To do Donation']:
        top = Toplevel(root)
        top.title(title)
        top.geometry("1980x1080")  

        # Load image
        image_path = r"D:\Vedant\Images\8.png"
        image = load_image(image_path)
        
        if image:
            canvas_top = Canvas(top, width=1980, height=1080)
            canvas_top.pack(fill=BOTH, expand=YES)
            canvas_top.create_image(0, 0, anchor=NW, image=image)
            # Keep a reference to avoid garbage collection
            canvas_top.image = image

            # Create a frame for form elements
            form_frame = Frame(canvas_top, bg="lightgray", bd=2, relief="sunken")
            form_frame.place(x=50, y=50, width=450, height=700)

            if title == 'To Plant Trees':
                # Create labels and entry widgets inside the form frame
                Label(form_frame, text="Enter your Name:", font=("Segoe UI Black", 15, "bold"), fg="brown", bg="lightyellow").grid(row=0, column=0, padx=10, pady=10, sticky=W)
                name_entry = Entry(form_frame)
                name_entry.grid(row=0, column=1, padx=10, pady=10)

                Label(form_frame, text="Enter your Email Address:", font=("Segoe UI Black", 15, "bold"), fg="yellow", bg="orange").grid(row=1, column=0, padx=10, pady=10, sticky=W)
                email_entry = Entry(form_frame)
                email_entry.grid(row=1, column=1, padx=10, pady=10)

                Label(form_frame, text="Date (DD-MM-YYYY):", font=("Segoe UI Black", 15, "bold"), fg="purple", bg="lavender").grid(row=2, column=0, padx=10, pady=10, sticky=W)
                date_entry = Entry(form_frame)
                date_entry.grid(row=2, column=1, padx=10, pady=10)

                Label(form_frame, text="Type of Tree 1:", font=("Segoe UI Black", 15, "bold"), fg="blue", bg="lightyellow").grid(row=3, column=0, padx=10, pady=10, sticky=W)
                tree_types = ["Neem", "Mesquite", "Peepal", "Desert willow", "Banyan", "Palo Verde", "Oak", "Willow", "Pine", "Maple", "Birch"]
                tree_combobox = ttk.Combobox(form_frame, values=tree_types)
                tree_combobox.grid(row=3, column=1, padx=10, pady=10)
        
                Label(form_frame, text="How many:", font=("Segoe UI Black", 15, "bold"), fg="purple", bg="lavender").grid(row=4, column=0, padx=10, pady=10, sticky=W)
                tree_entry = Entry(form_frame)
                tree_entry.grid(row=4, column=1, padx=10, pady=10)

                Label(form_frame, text="Type of Tree 2:", font=("Segoe UI Black", 15, "bold"), fg="brown", bg="lightyellow").grid(row=5, column=0, padx=10, pady=10, sticky=W)
                tree_type = ["Neem", "Mesquite", "Peepal", "Desert willow", "Banyan", "Palo Verde", "Oak", "Willow", "Pine", "Maple", "Birch"]
                trees_combobox = ttk.Combobox(form_frame, values=tree_type)
                trees_combobox.grid(row=5, column=1, padx=10, pady=10)

                Label(form_frame, text="How many:", font=("Segoe UI Black", 15, "bold"), fg="orange", bg="maroon").grid(row=6, column=0, padx=10, pady=10, sticky=W)
                tree_entrys = Entry(form_frame)
                tree_entrys.grid(row=6, column=1, padx=10, pady=10)

                # Button to display the information
                def display_info():
                    name = name_entry.get().strip()
                    email = email_entry.get().strip()
                    date = date_entry.get().strip()
                    tree_types = tree_combobox.get().strip()
                    number = tree_entry.get().strip()
                    tree_type = trees_combobox.get().strip()
                    num = tree_entrys.get().strip()

                    # Validate input
                    if not name or not email or not date or not tree_types or not number or not tree_type or not num:
                        messagebox.showerror("Input Error", "Please fill in all fields.")
                        return

                    # Validate email
                    if "@" not in email:
                        messagebox.showerror("Input Error", "Please enter a valid email address.")
                        return

                    # Validate numbers
                    if not (number.isdigit() and num.isdigit()):
                        messagebox.showerror("Input Error", "Please enter valid numbers for tree quantities.")
                        return
                    
                    number = int(number)
                    num = int(num)
                    total_trees = number + num

                    info = (f"Thank you for your contribution. \nYour information is:\n"
                            f"Your Name: {name}\n"
                            f"Your Email: {email}\n"
                            f"Date: {date}\n"
                            f"Type of Tree 1: {tree_types}\n"
                            f"Number of {tree_types} tree are: {number}\n"
                            f"Type of Tree 2: {tree_type}\n"
                            f"Number of {tree_type} tree are: {num}\n"
                            f"Total Number of Trees: {total_trees}")

                    info_label = Label(form_frame, text=info, font=("Cascadia Code", 12, "bold"), fg="darkgreen", bg="lightyellow")
                    info_label.grid(row=8, column=0, columnspan=2, padx=10, pady=10)

                Button(form_frame, text="Submit", command=display_info, font=("Agency FB", 16, "bold"), fg="lightyellow", bg="green").grid(row=7, column=0, columnspan=2, pady=20)

            elif title == 'To do Donation':
                # Create labels and entry widgets inside the form frame
                Label(form_frame, text="Enter your Name:", font=("Berlin Sans FB Demi", 15, "bold"), fg="brown", bg="lightyellow").grid(row=0, column=0, padx=10, pady=10, sticky=W)
                name_entry = Entry(form_frame)
                name_entry.grid(row=0, column=1, padx=10, pady=10)

                Label(form_frame, text="Enter your Email Address:", font=("Berlin Sans FB Demi", 15, "bold"), fg="orange", bg="maroon").grid(row=1, column=0, padx=10, pady=10, sticky=W)
                email_entry = Entry(form_frame)
                email_entry.grid(row=1, column=1, padx=10, pady=10)

                Label(form_frame, text="Date (DD-MM-YYYY):", font=("Berlin Sans FB Demi", 15, "bold"), fg="purple", bg="lavender").grid(row=2, column=0, padx=10, pady=10, sticky=W)
                date_entry = Entry(form_frame)
                date_entry.grid(row=2, column=1, padx=10, pady=10)

                Label(form_frame, text="Enter the Amount:", font=("Berlin Sans FB Demi", 15, "bold"), fg="blue", bg="lightyellow").grid(row=3, column=0, padx=10, pady=10, sticky=W)
                amount_entry = Entry(form_frame)
                amount_entry.grid(row=3, column=1, padx=10, pady=10)

                # Button to display the information
                def display_info():
                    name = name_entry.get().strip()
                    email = email_entry.get().strip()
                    date = date_entry.get().strip()
                    amount = amount_entry.get().strip()

                    # Validate input
                    if not name or not email or not date or not amount:
                        messagebox.showerror("Input Error", "Please fill in all fields.")
                        return

                    # Validate email
                    if "@" not in email:
                        messagebox.showerror("Input Error", "Please enter a valid email address.")
                        return

                    # Validate amount
                    if not amount.isdigit():
                        messagebox.showerror("Input Error", "Please enter a valid amount.")
                        return

                    infos = (f"Thank you for your contribution. \nYour information is:\n"
                             f"Your Name: {name}\n"
                             f"Your Email: {email}\n"
                             f"Date: {date}\n"
                             f"Your Contribution: {amount}")

                    infos_label = Label(form_frame, text=infos, font=("Cascadia Code", 12, "bold"), fg="darkgreen", bg="lightyellow")
                    infos_label.grid(row=4, column=0, columnspan=2, padx=10, pady=10)

                Button(form_frame, text="Submit", command=display_info, font=("Agency FB", 16, "bold"), fg="lightyellow", bg="green").grid(row=4, column=0, columnspan=2, pady=20)

    elif title == 'Reforestration':
        # Display 'Our Vision' content in the main window over the image
        canvas.delete("all")  # Clear existing content from the canvas
        
        image_path = r"D:\Vedant\Images\6.png"  # Use raw string to handle backslashes
        photo_image = load_image(image_path)
        if photo_image:
            canvas.create_image(0, 0, anchor=NW, image=photo_image)
            canvas.image = photo_image  # Keep a reference to avoid garbage collection

        # Title text on the canvas
        canvas.create_text(800, 150, text="Reforestration", font=("Showcard Gothic", 60, "bold", "underline"), fill="blue", anchor="n")

        # Description text on the canvas
        vision_description_text = (
        "Reforestation can be defined as the process of replanting trees in areas that have been affected by natural disturbances \nlike wildfires, drought, and insect and disease infestations — and unnatural ones like logging, mining, agricultural \nclearing, and development. This can mean anything from supporting natural regeneration in degraded areas to planting \necologically appropriate trees in areas that have seedlings after forest fires."
        )
        
        # Draw the text on top of the highlighted rectangle
        canvas.create_text(800, 300, text=vision_description_text, font=("Cascadia Code", 16, "bold"), fill="yellow", anchor="n", width=1600)

    elif title == 'Our Vision':
        # Display 'Our Vision' content in the main window over the image
        canvas.delete("all")  # Clear existing content from the canvas

        # Reload and display the main image
        image_path = r"D:\Vedant\Images\3.png"  # Use raw string to handle backslashes
        photo_image = load_image(image_path)
        if photo_image:
            canvas.create_image(0, 0, anchor=NW, image=photo_image)
            canvas.image = photo_image  # Keep a reference to avoid garbage collection

        # Title text on the canvas
        canvas.create_text(800, 150, text="OUR VISION", font=("Goudy Stout", 60, "bold", "underline"), fill="Yellow", anchor="n")

        # Description text on the canvas
        vision_description_text = (
            "We want to make it simple for anyone to help the environment by planting trees. Together we can restore forests, \ncreate habitat for biodiversity, and make a positive social impact around the world."
        )

        canvas.create_text(800, 300, text=vision_description_text, font=("Comic Sans MS", 16, "bold"), fill="red", anchor="n", width=1600)
    
    elif title == 'Our Model':
        # Display 'Our Vision' content in the main window over the image
        canvas.delete("all")  # Clear existing content from the canvas
        
        image_path = r"D:\Vedant\Images\4.png"  # Use raw string to handle backslashes
        photo_image = load_image(image_path)
        if photo_image:
            canvas.create_image(0, 0, anchor=NW, image=photo_image)
            canvas.image = photo_image  # Keep a reference to avoid garbage collection

        # Title text on the canvas
        canvas.create_text(800, 150, text="Our Model", font=("Showcard Gothic", 60, "bold", "underline"), fill="Yellow", anchor="n")

        # Description text on the canvas
        vision_description_text = (
        "One Tree Planted is an environmental nonprofit that is dedicated to making it simple for anyone to help the environment. \nOur simplified donation process and project transparency allow individuals, businesses and foundations to understand \nthe impact of their donation. But truthfully, planting trees is anything but simple. And as we often say, it’s about \nmore than planting trees. It’s about growing healthy forests. "
        )

        canvas.create_text(800, 300, text=vision_description_text, font=("Cascadia Code", 16, "bold"), fill="orange", anchor="n", width=1600)

    elif title == 'Contact us':
        # Display 'Our Vision' content in the main window over the image
        canvas.delete("all")  # Clear existing content from the canvas
        
        image_path = r"D:\Vedant\Images\7.png"  # Use raw string to handle backslashes
        photo_image = load_image(image_path)
        if photo_image:
            canvas.create_image(0, 0, anchor=NW, image=photo_image)
            canvas.image = photo_image  # Keep a reference to avoid garbage collection

        # Description text on the canvas
        vision_description_text = (
        "For more detailes contact us: 8103453857"
        )

        canvas.create_text(800, 300, text=vision_description_text, font=("Cascadia Code", 16, "bold"), fill="purple", anchor="n", width=1600)

    elif title == 'About':

        canvas.delete("all")  
        
        image_path = r"D:\Vedant\Images\8.png" 
        photo_image = load_image(image_path)
        if photo_image:
            canvas.create_image(0, 0, anchor=NW, image=photo_image)
            canvas.image = photo_image  

        canvas.create_text(150, 180, text="About Us", font=("Showcard Gothic", 30, "bold", "underline"), fill="Yellow", anchor="n")

        vision_description_text = (
        "Welcome to Reforestration, where our commitment to reforestation and environmental stewardship drives us to make a \ntangible impact on the world."
        )

        canvas.create_text(750, 240, text=vision_description_text, font=("Cascadia Code", 16, "bold"), fill="lavender", anchor="n", width=1600)

        canvas.create_text(180, 320, text="Our Mission", font=("Showcard Gothic", 30, "bold", "underline"), fill="Lightyellow", anchor="n")

        vision_description_text = (
        "At this organization, we believe in the transformative power of trees to restore ecosystems, combat climate change, and \nenhance the quality of life for communities around the globe. Our mission is to replant and rehabilitate forests that \nhave been lost due to deforestation, natural disasters, and human activities. We strive to create a greener, healthier \nplanet through innovative reforestation projects and community engagement."
        )

        canvas.create_text(775, 380, text=vision_description_text, font=("Cascadia Code", 16, "bold"), fill="pink", anchor="n", width=1600)

        canvas.create_text(170, 520, text="By Vedant Vyas\nThank You", font=("Showcard Gothic", 20, "bold"), fill="orange", anchor="n")

# Create the main window
root = Tk()
root.title("Reforestration")

# Create a frame to hold the canvas
main_frame = Frame(root)
main_frame.pack(fill=BOTH, expand=YES)

# Create a canvas for the image
canvas = Canvas(main_frame, width=1920, height=1080)
canvas.pack(fill=BOTH, expand=YES)

# Load and display the image
image_path = r"D:\Vedant\Images\5.png" 
photo_image = load_image(image_path)
if photo_image:
    canvas.create_image(0, 0, anchor=NW, image=photo_image)
    # Keep a reference to avoid garbage collection
    canvas.image = photo_image

# Description text on the canvas
description_text = (
"                                           Welcome to Reforestration! 🌱\n"
"Thank you for visiting our hub for reforestation and environmental stewardship. Here, we believe in the power of trees \nto heal our planet, enrich our communities, and inspire a brighter future. \nExplore our site to discover how you can join the movement to restore forests, support local ecosystems, and make a \ntangible impact. Whether you're looking to get involved, learn more, or contribute to our mission, we’re excited to \nhave you on this journey with us. \nTogether, let's plant the seeds for a greener tomorrow."
)

canvas.create_text(790, 300, text=description_text, font=("Cascadia Code", 16, "bold"), fill="darkgreen", anchor="n", width=1600)

# Create the menu bar
menu = Menu(root)
root.config(menu=menu)

# Create menus
home_menu = Menu(menu, tearoff=0)
filemenu = Menu(menu, tearoff=0)
aboutmenu = Menu(menu, tearoff=0)
helpmenu = Menu(menu, tearoff=0)

def go_home():
    canvas.delete("all")  # Clear existing content from the canvas
    photo_image = load_image(r"D:\Vedant\Images\5.png")  # Reload the home image
    if photo_image:
        canvas.create_image(0, 0, anchor=NW, image=photo_image)
        canvas.image = photo_image  # Keep a reference to avoid garbage collection
    canvas.create_text(790, 300, text=description_text, font=("Cascadia Code", 16, "bold"), fill="red", anchor="n", width=1600)

menu.add_cascade(label='Home', menu=home_menu)
home_menu.add_command(label='Home', command=go_home)

# Configure menu items
menu.add_cascade(label='Join Us', menu=filemenu)
filemenu.add_command(label='To Plant Trees', command=lambda: open_top_level('To Plant Trees'))
filemenu.add_command(label='To do Donation', command=lambda: open_top_level('To do Donation'))
filemenu.add_separator()
filemenu.add_command(label='Exit', command=root.quit)

menu.add_cascade(label='About', menu=aboutmenu)
aboutmenu.add_command(label='Reforestration', command=lambda: open_top_level('Reforestration'))
aboutmenu.add_command(label='Our Vision', command=lambda: open_top_level('Our Vision'))
aboutmenu.add_command(label='Our Model', command=lambda: open_top_level('Our Model'))

menu.add_cascade(label='Help', menu=helpmenu)
helpmenu.add_command(label='Contact us', command=lambda: open_top_level('Contact us'))
helpmenu.add_command(label='About', command=lambda: open_top_level('About'))

# Start the Tkinter event loop
root.mainloop()
