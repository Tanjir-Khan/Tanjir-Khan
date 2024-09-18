

# Load the previously saved presentation
prs = Presentation(pptx_file_updated)

# Load the football-themed background image for use in slides
background_image = "/mnt/data/A_dynamic_football-themed_PowerPoint_slide_backgro.png"

# Function to add background to a slide
def apply_background(slide):
    slide.shapes.add_picture(background_image, 0, 0, width=prs.slide_width, height=prs.slide_height)

# Function to add an image to a slide with specified size
def add_image(slide, image_path, left, top, width, height):
    slide.shapes.add_picture(image_path, Inches(left), Inches(top), width=Inches(width), height=Inches(height))

# Apply the background to all content slides (excluding title slide)
for slide_idx in range(1, len(prs.slides)):
    slide = prs.slides[slide_idx]
    apply_background(slide)

# Adding logos and team icons
logos = {
    "Bundesliga": "/mnt/data/bundesliga_logo.png",  # Placeholder for Bundesliga logo
    "La Liga": "/mnt/data/laliga_logo.png",  # Placeholder for La Liga logo
    "Ligue 1": "/mnt/data/ligue1_logo.png",  # Placeholder for Ligue 1 logo
    "Serie A": "/mnt/data/seriea_logo.png",  # Placeholder for Serie A logo
    "Saudi Pro League": "/mnt/data/saudi_league_logo.png",  # Placeholder for Saudi League logo
    "Champions League": "/mnt/data/champions_league_logo.png"  # Placeholder for UCL logo
}

# Placeholder for adding images and logos (representative positions for each slide)
logo_positions = {
    3: ("Bundesliga", 8.5, 0.5),  # Bundesliga slide
    4: ("La Liga", 8.5, 0.5),  # La Liga slide
    5: ("Ligue 1", 8.5, 0.5),  # Ligue 1 slide
    6: ("Serie A", 8.5, 0.5),  # Serie A slide
    7: ("Saudi Pro League", 8.5, 0.5),  # Saudi Pro League slide
    8: ("Champions League", 8.5, 0.5)  # UCL slide
}

# Add logos for each league
for slide_idx, (league, pos_left, pos_top) in logo_positions.items():
    logo_image_path = logos.get(league)
    if logo_image_path:
        slide = prs.slides[slide_idx]
        add_image(slide, logo_image_path, pos_left, pos_top, 1.5, 1.5)

# Adding player spotlights (one player per league)
players = {
    3: ("/mnt/data/lewandowski_bayern.png", "Robert Lewandowski", "Bayern Munich"),
    4: ("/mnt/data/messi_barcelona.png", "Lionel Messi", "Barcelona"),
    5: ("/mnt/data/mbappe_psg.png", "Kylian Mbappé", "Paris Saint-Germain"),
    6: ("/mnt/data/ronaldo_juventus.png", "Cristiano Ronaldo", "Juventus"),
    7: ("/mnt/data/ronaldo_alnassr.png", "Cristiano Ronaldo", "Al Nassr"),
    8: ("/mnt/data/haaland_mancity.png", "Erling Haaland", "Manchester City")
}

# Add player spotlight for each league
for slide_idx, (player_image, player_name, team) in players.items():
    slide = prs.slides[slide_idx]
    # Add player image
    add_image(slide, player_image, 0.5, 2, 2, 2)
    # Add player name and team
    text_box = slide.shapes.add_textbox(Inches(0.5), Inches(4.2), Inches(4), Inches(1))
    tf = text_box.text_frame
    tf.text = f"{player_name} - {team}"
    text_box.text_frame.paragraphs[0].font.size = Pt(18)
    text_box.text_frame.paragraphs[0].font.bold = True
    text_box.text_frame.paragraphs[0].font.color.rgb = RGBColor(255, 255, 255)

# Adding fun facts for each league on their respective slides
fun_facts = {
    3: "Bayern Munich has won the Bundesliga title 32 times, the most in the league's history.",
    4: "FC Barcelona and Real Madrid have won La Liga over 60 times combined.",
    5: "Paris Saint-Germain has dominated Ligue 1 with 10 titles since 2013.",
    6: "Juventus won nine consecutive Serie A titles between 2011-2020.",
    7: "Cristiano Ronaldo joined Al-Nassr in 2023, boosting the Saudi Pro League's popularity.",
    8: "The Champions League is the most prestigious club tournament in Europe, won by Real Madrid 14 times."
}

for slide_idx, fact in fun_facts.items():
    slide = prs.slides[slide_idx]
    text_box = slide.shapes.add_textbox(Inches(0.5), Inches(5.2), Inches(6), Inches(1))
    tf = text_box.text_frame
    tf.text = "Fun Fact: " + fact
    text_box.text_frame.paragraphs[0].font.size = Pt(14)
    text_box.text_frame.paragraphs[0].font.bold = True
    text_box.text_frame.paragraphs[0].font.color.rgb = RGBColor(255, 255, 255)

# Save the enhanced presentation
pptx_file_final = "/mnt/data/Enhanced_Football_Leagues_Presentation.pptx"
prs.save(pptx_file_final)

pptx_file_final
