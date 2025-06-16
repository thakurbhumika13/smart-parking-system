import random
import time
import sqlite3

def simulate_sensor():
    while True:
        slot_id = random.randint(1, 10)
        status = random.choice(["Occupied", "Available"])
        
        conn = sqlite3.connect("db/parking.db")
        cursor = conn.cursor()
        cursor.execute("UPDATE slots SET status = ? WHERE id = ?", (status, slot_id))
        conn.commit()
        conn.close()
        
        print(f"Slot {slot_id} -> {status}")
        time.sleep(5)  # simulate every 5 seconds

if __name__ == "__main__":
    simulate_sensor()
// pseudo-code
if (carDetected) {
    sendHttpPost("http://<flask-server>/update_slot", data);
}
@app.route('/update_slot', methods=['POST'])
def update_slot():
    slot_id = request.json['slot_id']
    status = request.json['status']
    # update DB
