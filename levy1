import time
import random
import sys

# --- DATABASE: คลังคำศัพท์อักษรเวท ---
WORD_DATABASE = {
    "LIGHT": {
        "word": "LIGHT", "thai": "แสงสว่าง", "pos": "Noun/Adj", "tier": "A1", "cat": "ธรรมชาติ",
        "sentence": "The magical LIGHT chased away the darkness.", "synonym": "BRIGHT", "bonus": 10
    },
    "BRIGHT": {
        "word": "BRIGHT", "thai": "สว่างไสว", "pos": "Adj", "tier": "A2", "cat": "ธรรมชาติ",
        "sentence": "A BRIGHT crystal illuminates the entire room.", "synonym": "RADIANT", "bonus": 25
    },
    "RADIANT": {
        "word": "RADIANT", "thai": "เปล่งประกายเจิดจ้า", "pos": "Adj", "tier": "C1", "cat": "ธรรมชาติ",
        "sentence": "She cast a RADIANT shield that blinded the monsters.", "synonym": None, "bonus": 60
    },
    "WARM": {
        "word": "WARM", "thai": "อบอุ่น", "pos": "Adj", "tier": "A1", "cat": "ความรู้สึก",
        "sentence": "A WARM blanket was created from the letters.", "synonym": "COZY", "bonus": 10
    },
    "COZY": {
        "word": "COZY", "thai": "อบอุ่นและสบาย", "pos": "Adj", "tier": "B1", "cat": "ความรู้สึก",
        "sentence": "The cafe provides a COZY atmosphere for adventurers.", "synonym": "COMFORTABLE", "bonus": 30
    },
    "COMFORTABLE": {
        "word": "COMFORTABLE", "thai": "สุขสบาย/ไร้กังวล", "pos": "Adj", "tier": "A2", "cat": "ความรู้สึก",
        "sentence": "He sat on a COMFORTABLE chair made of cloud magic.", "synonym": None, "bonus": 50
    },
    "HEAL": {
        "word": "HEAL", "thai": "รักษา/เยียวยา", "pos": "Verb", "tier": "A2", "cat": "เยียวยา",
        "sentence": "The word HEAL mended the broken wings of the fairy.", "synonym": "COMFORT", "bonus": 15
    },
    "COMFORT": {
        "word": "COMFORT", "thai": "ปลอบใจ/บรรเทาทุกข์", "pos": "Verb/Noun", "tier": "B1", "cat": "เยียวยา",
        "sentence": "Soft music was played to COMFORT the sad king.", "synonym": "SOOTHE", "bonus": 35
    },
    "SOOTHE": {
        "word": "SOOTHE", "thai": "บรรเทา/ทำให้สงบลง", "pos": "Verb", "tier": "C1", "cat": "เยียวยา",
        "sentence": "The magic script helped to SOOTHE the crying baby dragon.", "synonym": None, "bonus": 65
    }
}

# --- DATABASE: ลูกค้าและเควสต์ ---
CUSTOMER_POOL = [
    {
        "name": "คุณยายมารี (ชาวบ้าน)",
        "dialog": "ช่วงนี้พายุเข้า บ้านของยายมัน **มืดมนและวังเวง** เหลือเกิน ไม่อยากอยู่คนเดียวในความมืดเลยจ้า...",
        "target_base": "LIGHT",
        "all_valid": ["LIGHT", "BRIGHT", "RADIANT"],
        "hint_word": "LIGHT (แสงสว่าง)"
    },
    {
        "name": "อัศวินฝึกหัด อัลเบิร์ต",
        "dialog": "วันนี้ไปลุยดันเจี้ยนหิมะมา ร่างกายผม **หนาวสั่นไปหมด** อยากได้อะไรที่ทำให้รู้สึกผ่อนคลายในเตาผิงจังครับ...",
        "target_base": "WARM",
        "all_valid": ["WARM", "COZY", "COMFORTABLE"],
        "hint_word": "WARM (อบอุ่น)"
    },
    {
        "name": "เอลฟ์สาว ลิเนียร์",
        "dialog": "สัตว์เลี้ยงของฉันเพิ่งจากไป... หัวใจของฉันมัน **แตกสลายและเศร้าหมอง** เหลือเกิน พอจะมีอะไรช่วยฉันได้ไหม...",
        "target_base": "HEAL",
        "all_valid": ["HEAL", "COMFORT", "SOOTHE"],
        "hint_word": "HEAL (รักษา)"
    }
]

# --- PLAYER STATE: สถานะผู้เล่น ---
player = {
    "gold": 50,
    "cafe_exp": 0,
    "cafe_level": 1,
    "proficiency": {w: 0 for w in WORD_DATABASE}, # เก็บเลเวลความคุ้นเคยของแต่ละคำ
    "unlocked_words": ["LIGHT", "WARM", "HEAL"] # เริ่มต้นปลดล็อกคำระดับ A1/A2
}

def print_slow(text, speed=0.01):
    for char in text:
        sys.stdout.write(char)
        sys.stdout.flush()
        time.sleep(speed)
    print()

def draw_line():
    print("━" * 60)

# --- SYSTEM: แอนิเมชันเสกเวทมนตร์ (Solid Script Effect) ---
def animate_solid_script(word):
    print("\n✨ [เริ่มการร่ายเวทอักษร Solid Script] ✨")
    time.sleep(0.4)
    print_slow(f"✍️  คุณเริ่มตวัดนิ้วกลางอากาศ ร่างอักษรเรืองแสง: ", 0.02)
    
    # เอฟเฟกต์ตัวอักษรค่อยๆ ปรากฏ
    for char in word:
        print(f" {char} ", end="", flush=True)
        time.sleep(0.2)
    print()
    
    time.sleep(0.3)
    print(f"🔮 [Solid Script: {word}!!]")
    print(f"✨ ตัวอักษรสามมิติกลายเป็นวัตถุเวทมนตร์รูปพลังงานลอยเด่นขึ้นมา! ✨\n")
    time.sleep(0.5)

# --- MODE 1: สมุดสูตรอบอักษรเวท (Magic Recipe Book) ---
def open_recipe_book():
    while True:
        draw_line()
        print("📖 [ สมุดสูตรอบอักษรเวท - The Magic Recipe Book ] 📖")
        print("ดูคำศัพท์และทดลองเสกใน Sandbox")
        draw_line()
        
        # แสดงรายการคำศัพท์ที่ปลดล็อกแล้ว
        for i, w_key in enumerate(player["unlocked_words"], 1):
            w_info = WORD_DATABASE[w_key]
            prof_lvl = player["proficiency"][w_key]
            print(f"{i}. {w_info['word']} ({w_info['tier']}) - แปลว่า: {w_info['thai']} [ระดับความคุ้นเคย: Lvl {prof_lvl}/3]")
        
        print(f"{len(player['unlocked_words']) + 1}. กลับหน้าหลัก")
        
        choice = input("\nเลือกคำศัพท์เพื่อดูรายละเอียด / ทดลองเสก (พิมพ์ตัวเลข): ")
        if choice.isdigit():
            idx = int(choice) - 1
            if idx == len(player["unlocked_words"]):
                break
            elif 0 <= idx < len(player["unlocked_words"]):
                w_key = player["unlocked_words"][idx]
                w_info = WORD_DATABASE[w_key]
                
                # แสดงรายละเอียดคำศัพท์
                draw_line()
                print(f"🔍 ข้อมูลอักษรเวท: [{w_info['word']}]")
                print(f"ประเภทคำ: {w_info['pos']} | หมวดหมู่: {w_info['cat']} | ระดับ: {w_info['tier']}")
                print(f"ความหมาย: {w_info['thai']}")
                print(f"ตัวอย่างประโยคใช้งาน (Context): \"{w_info['sentence']}\"")
                if w_info['synonym']:
                    prof_req = "ปลดล็อกแล้ว" if player["proficiency"][w_key] >= 3 else "ต้องการระดับความคุ้นเคย Lvl 3 เพื่อปลดล็อก"
                    print(f"คำศัพท์หรูขั้นถัดไป (Synonym): {w_info['synonym']} ({prof_req})")
                else:
                    print("คำศัพท์นี้อยู่ในระดับสูงสุดของสายนี้แล้ว!")
                draw_line()
                
                sandbox = input("ต้องการกดปุ่ม [ลองเสก] (Vocabulary Sandbox) หรือไม่? (y/n): ")
                if sandbox.lower() == 'y':
                    animate_solid_script(w_info['word'])
                    print_slow(f"💡 ข้อแนะนำการใช้: {w_info['sentence']}")
                    input("\nกด Enter เพื่อดำเนินการต่อ...")
            else:
                print("❌ ไม่มีหมายเลขนี้ในสมุด")
        else:
            print("❌ กรุณากรอกตัวเลข")

# --- MODE 2: เปิดร้านคาเฟ่คำพูด (Cafe Simulation) ---
def open_cafe():
    draw_line()
    print("☕ คาเฟ่ต่างโลก Word & Craft Cafe เปิดบริการแล้ว! ☕")
    draw_line()
    time.sleep(0.5)
    
    # สุ่มลูกค้า 1 คนต่อการเปิดร้าน
    customer = random.choice(CUSTOMER_POOL)
    print_slow(f"🔔 กริ๊ง~ ลูกค้าท่านหนึ่งเดินเข้ามาในร้าน... เขาคือ [{customer['name']}]")
    print_slow(f"💬 {customer['name']}: \"{customer['dialog']}\"")
    
    # สถานะการใช้คำใบ้
    hint_level = 0
    
    while True:
        print("\n[ เมนูคำสั่งผู้เล่น ]")
        print("1. ✍️  ลงมือพิมพ์คำศัพท์เวทมนตร์เสกของ")
        print(f"2. 🧠 ใช้ ดิกชันนารีในใจ (Mental Dictionary) [ใบ้ระดับ 2 - ฟรี]")
        print(f"3. 🍵 เสิร์ฟ ชาสมุนไพรเรียกไอเดีย (Inspiration Tea) [ใบ้ระดับ 3 - จ่าย 15 Gold]")
        print("4. 🚪 ขอโทษลูกค้า (ปฏิเสธเควสต์)")
        
        action = input("เลือกสิ่งที่คุณต้องการทำ (1-4): ")
        
        if action == "1":
            print("\n*พิมพ์คำศัพท์ภาษาอังกฤษที่คุณต้องการเสก (ตัวพิมพ์เล็กหรือใหญ่ก็ได้)*")
            player_word = input("คำศัพท์เวทมนตร์ของคุณคือ: ").upper()
            
            if player_word in customer["all_valid"]:
                if player_word in player["unlocked_words"]:
                    # คำตอบถูกต้องและปลดล็อกแล้ว
                    w_info = WORD_DATABASE[player_word]
                    animate_solid_script(player_word)
                    
                    # คำนวณรางวัล
                    reward_gold = 20 + w_info["bonus"]
                    reward_exp = 15 + (10 if w_info["tier"] != "A1" else 0)
                    
                    player["gold"] += reward_gold
                    player["cafe_exp"] += reward_exp
                    
                    print_slow(f"🎉 {customer['name']} ประทับใจมาก! ได้รับพลังเวท [{player_word}] เข้าไปเยียวยาจิตใจ")
                    print(f"💰 ได้รับเงิน: {reward_gold} Gold | ✨ ได้รับ EXP คาเฟ่: {reward_exp}")
                    
                    # ระบบเพิ่มความคุ้นเคยคำศัพท์ (Proficiency)
                    player["proficiency"][player_word] = min(3, player["proficiency"][player_word] + 1)
                    print(f"📈 ค่าความคุ้นเคยของคำว่า [{player_word}] เพิ่มขึ้นเป็น Lvl {player["proficiency"][player_word]}/3")
                    
                    # เช็คเงื่อนไขปลดล็อกคำศัพท์หรู (Synonyms)
                    if player["proficiency"][player_word] >= 3 and w_info["synonym"]:
                        syn = w_info["synonym"]
                        if syn not in player["unlocked_words"]:
                            player["unlocked_words"].append(syn)
                            print(f"🔥 ยอดเยี่ยม! คุณเชี่ยวชาญคำว่า {player_word} จนปลดล็อกคำศัพท์หรูขั้นถัดไป: [{syn}] ({WORD_DATABASE[syn]['tier']}) เข้าสมุดสูตรแล้ว!")
                    
                    # เช็คเลเวลอัปคาเฟ่
                    if player["cafe_exp"] >= player["cafe_level"] * 40:
                        player["cafe_level"] += 1
                        print(f"🌟 คาเฟ่เลเวลอัป! ตอนนี้คาเฟ่ของคุณเลเวล {player['cafe_level']} แล้ว!")
                        
                    break
                else:
                    print(f"❌ คุณรู้คำศัพท์คำนี้ แต่ในตัวเกมคุณยังไม่ได้ศึกษาหรือปลดล็อกมันในระบบ! (ไปเก็บเลเวลคำศัพท์ก่อนหน้าให้ถึง Lvl 3 ในร้านก่อนนะ)")
            else:
                print(f"❌ คำว่า {player_word} ไม่สามารถช่วยแก้ปัญหาให้ลูกค้าตรงจุดได้ ลองใหม่อีกครั้ง!")
                
        elif action == "2":
            # ใบ้ระดับ 2: บอกตัวแรกและจำนวนอักษร
            target = customer["target_base"]
            masked = target[0] + " " + "_ " * (len(target) - 1)
            print(f"\n🧠 [Mental Dictionary]: คุณนึกขึ้นได้ว่าคำพื้นฐานขึ้นต้นด้วยอักษรประมาณนี้: ({masked})")
            print(f"คำแปล: {WORD_DATABASE[target]['thai']}")
            
        elif action == "3":
            # ใบ้ระดับ 3: ชาสมุนไพรเรียกไอเดีย
            if player["gold"] >= 15:
                player["gold"] -= 15
                target = customer["target_base"]
                print("\n🍵 คุณเสิร์ฟชาสมุนไพรร้อนๆ สูตรพิเศษ... ภูตอักษรตัวจิ๋วบินไปช่วยนวดไหล่ให้ลูกค้า")
                print_slow(f"🧚 ภูตจิ๋วเฉลยคำใบ้ตรงๆ: \"คำพื้นฐานคือคำว่า {customer['hint_word']} จ้า!\"")
                print(f"💡 (หากคุณปลดล็อกคำศัพท์หรูอย่างคำว่า {WORD_DATABASE[target].get('synonym')} ในสมุดแล้ว ลองนำมาใช้สิ จะได้เงินและเลเวลเพิ่มขึ้นนะ!)")
                print(f"💸 เสียค่าชาไป 15 Gold (เหลือเงิน {player['gold']} Gold)")
            else:
                print("\n❌ เงินของคุณมีไม่พอจ่ายค่าชาสมุนไพร (ต้องการ 15 Gold)")
                
        elif action == "4":
            print_slow(f"\n🚪 คุณกล่าวขอโทษลูกค้า... {customer['name']} เดินออกจากร้านไปด้วยความเสียดาย")
            break
        else:
            print("❌ คำสั่งไม่ถูกต้อง")
            
    input("\nกด Enter เพื่อปิดร้านในวันนี้...")

# --- MAIN LOOP: เมนูหลักของเกม ---
def main_game():
    while True:
        draw_line()
        print(f"🧙‍♂️  ยินดีต้อนรับสู่ Word & Craft Cafe | เลเวลร้าน: Lvl {player['cafe_level']} | เงิน: {player['gold']} Gold")
        print("ถอดรหัสเวทมนตร์อักษร Solid Script ของเลวี่ แมคการ์เดน!")
        draw_line()
        print("1. 📖 เปิดดู 'สมุดสูตรอบอักษรเวท' (ดูหมวดคำศัพท์ / โหมดทดลองเสก Sandbox)")
        print("2. ☕ เปิดร้านคาเฟ่ต้อนรับลูกค้า (เล่นโหมดเนื้อเรื่องและฝึกภาษา)")
        print("3. 📊 ตรวจสอบสถานะจอมเวทอักษรศาสตร์ของคุณ")
        print("4. 🚪 ออกจากเกม")
        draw_line()
        
        choice = input("เลือกเมนูที่ต้องการ (1-4): ")
        
        if choice == "1":
            open_recipe_book()
        elif choice == "2":
            open_cafe()
        elif choice == "3":
            draw_line()
            print("📊 [ สถานะผู้เล่นและคลังความรู้ ]")
            print(f"• เลเวลคาเฟ่: Lvl {player['cafe_level']} (EXP: {player['cafe_exp']})")
            print(f"• เงินที่มีในกระเป๋า: {player['gold']} Gold")
            print("• ระดับความคุ้นเคยของคำศัพท์ที่เรียนรู้แล้ว:")
            for w in player["unlocked_words"]:
                print(f"   - {w} ({WORD_DATABASE[w]['tier']}): ระดับ Lvl {player['proficiency'][w]}/3")
            input("\nกด Enter เพื่อกลับเมนูหลัก...")
        elif choice == "4":
            print("ขอบคุณที่มาร่วมร่ายเวทมนตร์อักษร คาเฟ่ปิดบริการแล้วจ้า! บ๊ายบาย ✨")
            break
        else:
            print("❌ กรุณาเลือกเมนู 1-4 ให้ถูกต้อง")

# เริ่มรันเกม
if __name__ == "__main__":
    main_game()
