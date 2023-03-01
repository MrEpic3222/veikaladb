# veikaladb
db
import sqlite3


conn = sqlite3.connect('veikala_db.db')
c = conn.cursor()

# Izveidojam tabulas
c.execute('''CREATE TABLE IF NOT EXISTS produkts
             (produkta_id INTEGER PRIMARY KEY, produkta_nosaukums TEXT, cena REAL)''')

c.execute('''CREATE TABLE IF NOT EXISTS pasutijums
             (pasutijuma_id INTEGER PRIMARY KEY, pasutijuma_datums DATE, piegade INTEGER)''')

c.execute('''CREATE TABLE IF NOT EXISTS pasutijuma_preces
             (pasutijuma_id INTEGER, produkta_id INTEGER, daudzums INTEGER,
              FOREIGN KEY (pasutijuma_id) REFERENCES pasutijums(pasutijuma_id),
              FOREIGN KEY (produkta_id) REFERENCES produkts(produkta_id))''')

# Pievienojam preces datubāzei
c.execute("INSERT INTO produkts VALUES (1, 'Bumbieris', 1.25)")
c.execute("INSERT INTO produkts VALUES (2, 'Banāns', 0.50)")
c.execute("INSERT INTO produkts VALUES (3, 'Ābols', 0.75)")
c.execute("INSERT INTO produkts VALUES (4, 'Mango', 1.15)")
c.execute("INSERT INTO produkts VALUES (5, 'Siers', 3.15)")
c.execute("INSERT INTO produkts VALUES (6, 'Šokolade', 2.15)")
# Pievienojam pasūtījumus datubāzei
c.execute("INSERT INTO pasutijums VALUES (1, '2022-01-01', 1)")
c.execute("INSERT INTO pasutijums VALUES (2, '2022-01-05', 0)")

# Pievienojam preces pasūtījumiem datubāzē
c.execute("INSERT INTO pasutijuma_preces VALUES (1, 1, 2)")
c.execute("INSERT INTO pasutijuma_preces VALUES (1, 2, 3)")
c.execute("INSERT INTO pasutijuma_preces VALUES (2, 3, 1)")
c.execute("INSERT INTO pasutijuma_preces VALUES (2, 4, 2)")


conn.commit()
conn.close()
