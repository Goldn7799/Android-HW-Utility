# 1. Verifikasi Akses Root
if [ "$(id -u)" -ne 0 ]; then
    echo "[!] Error: Script ini memerlukan akses Root (su)."
    exit 1
fi

echo "=========================================="
echo "      CPU Core Auto-Online Script         "
echo "=========================================="

# 2. Deteksi Total Core CPU secara Dinamis
TOTAL_CORES=$(ls -d /sys/devices/system/cpu/cpu[0-9]* 2>/dev/null | wc -l)

if [ "$TOTAL_CORES" -eq 0 ]; then
    echo "[!] Error: Gagal mendeteksi core CPU."
    exit 1
fi

echo "[i] Total Core terdeteksi: $TOTAL_CORES Core"
echo "------------------------------------------"

ACTIVATED=0
ALREADY_ONLINE=0

# 3. Loop Pengecekan & Pengaktifan
i=0
while [ $i -lt $TOTAL_CORES ]; do
    ONLINE_FILE="/sys/devices/system/cpu/cpu$i/online"
    
    # cpu0 umumnya master core (selalu online dan tidak memiliki file 'online')
    if [ -f "$ONLINE_FILE" ]; then
        STATUS=$(cat "$ONLINE_FILE" 2>/dev/null)
        
        if [ "$STATUS" -eq 0 ]; then
            echo "[+] CPU $i: OFFLINE -> Mengaktifkan..."
            echo 1 > "$ONLINE_FILE"
            
            # Verifikasi status setelah dinyalakan
            NEW_STATUS=$(cat "$ONLINE_FILE" 2>/dev/null)
            if [ "$NEW_STATUS" -eq 1 ]; then
                echo "    -> [BERHASIL] CPU $i sekarang ONLINE."
                ACTIVATED=$((ACTIVATED + 1))
            else
                echo "    -> [GAGAL] CPU $i tidak bisa diubah (dikunci kernel/thermal)."
            fi
        else
            echo "[-] CPU $i: SUDAH ONLINE"
            ALREADY_ONLINE=$((ALREADY_ONLINE + 1))
        fi
    else
        echo "[-] CPU $i: ONLINE (Primary Core)"
        ALREADY_ONLINE=$((ALREADY_ONLINE + 1))
    fi
    
    i=$((i + 1))
done

# 4. Ringkasan
echo "------------------------------------------"
echo "[i] Ringkasan:"
echo "    - Core diaktifkan : $ACTIVATED"
echo "    - Core sudah aktif: $ALREADY_ONLINE"
echo "=========================================="
