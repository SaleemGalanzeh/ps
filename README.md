Methodology 
First-Come, First-Served (FCFS) – Non-Preemptive 
class Process:
def __init__(self, pid, burst_time, third_param): 
self.pid = pid
self.burst_time = burst_time self.third_param = third_param 
def FCFS(processes):
n = len(processes) waiting_time = [0] * n turnaround_time = [0] * n waiting_time[0] = 0 
# Calculate waiting time for each process for i in range(1, n): 
waiting_time[i] = processes[i-1].burst_time + waiting_time[i-1] 
# Calculate turnaround time for each process for i in range(n): 
turnaround_time[i] = processes[i].burst_time + waiting_time[i] 
print("Processes Burst Time Waiting Time Turnaround Time") for i in range(n): 
print(processes[i].pid, processes[i].burst_time, waiting_time[i], turnaround_time[i]) 
avg_wt = sum(waiting_time) / n avg_tat = sum(turnaround_time) / n return avg_wt, avg_tat 
# Main
process_data = [(1, 10, 0), (2, 5, 0), (3, 8, 0)]
processes = [Process(pid, burst_time, third_param) for pid, burst_time, third_param in process_data]
avg_wt, avg_tat = FCFS(processes)
print("Average Waiting Time:", avg_wt)
print("Average Turnaround Time:", avg_tat) 



Shortest-Job-First (SJF) – Non-Preemptive 
class Process:
def __init__(self, pid, burst_time, third_param): 
self.pid = pid
self.burst_time = burst_time self.third_param = third_param 
def SJF_NonPreemptive(processes):
n = len(processes) processes.sort(key=lambda x: x.burst_time) waiting_time = [0] * n 
turnaround_time = [0] * n 
# Calculate waiting time for each process for i in range(1, n): 
waiting_time[i] = processes[i-1].burst_time + waiting_time[i-1] 
# Calculate turnaround time for each process for i in range(n): 
turnaround_time[i] = processes[i].burst_time + waiting_time[i] 
print("Processes Burst Time Waiting Time Turnaround Time") for i in range(n): 
print(processes[i].pid, processes[i].burst_time, waiting_time[i], turnaround_time[i]) 
avg_wt = sum(waiting_time) / n avg_tat = sum(turnaround_time) / n return avg_wt, avg_tat 
# Main
process_data = [(1, 10, 0), (2, 5, 0), (3, 8, 0)]
processes = [Process(pid, burst_time, third_param) for pid, burst_time, third_param in process_data]
avg_wt, avg_tat = SJF_NonPreemptive(processes)
print("Average Waiting Time:", avg_wt)
print("Average Turnaround Time:", avg_tat) 











Shortest-Remaining-Time-First (SRTF): 
def findWaitingTime(processes, n, wt): rt = [0] * n
for i in range(n): 
rt[i] = processes[i][1] 
complete = 0
t=0 #currenttime minm = float('inf') short = 0
check = False 
while complete != n: for j in range(n): 
if processes[j][2] <= t and rt[j] < minm and rt[j] > 0: minm = rt[j]
short = j
check = True 
if not check: t += 1 
continue 
rt[short] -= 1
minm = rt[short] if rt[short] > 0 else float('inf') 
if rt[short] == 0:
complete += 1
check = False
finish_time = t + 1
wt[short] = finish_time - processes[short][1] - processes[short][2] 
if wt[short] < 0: wt[short] = 0 
t += 1 
def findTurnAroundTime(processes, n, wt, tat): for i in range(n): 
tat[i] = processes[i][1] + wt[i] 
def findavgTime(processes, n): wt = [0] * n
tat = [0] * n 
findWaitingTime(processes, n, wt) findTurnAroundTime(processes, n, wt, tat) 
total_wt = 0 total_tat = 0 
print("Processes Burst Time Arrival Time Waiting Time Turnaround Time") for i in range(n): 
total_wt += wt[i]
total_tat += tat[i]
print(f" {i+1}\t\t{processes[i][1]}\t\t{processes[i][2]}\t\t{wt[i]}\t\t{tat[i]}") 
print(f"\nAverage Waiting Time = {total_wt / n:.2f}") print(f"Average Turnaround Time = {total_tat / n:.2f}") 
# Main
processes = [(1, 6, 2), (2, 8, 5), (3, 7, 1), (4, 3, 0)] n = len(processes)
findavgTime(processes, n) 
