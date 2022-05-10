#1.SystemInfo::Init

```
SystemInfo::Init
--struct tms time_sample;                   
--char line[128];                           
--last_cpu_ = times(&time_sample);          
--last_sys_cpu_ = time_sample.tms_stime;    
--last_user_cpu_ = time_sample.tms_utime;   
--num_processors_ = 0;                      
--FILE* file = fopen("/proc/cpuinfo", "r"); 
--if (file) {
            while (fgets(line, 128, file) != nullptr) {
                if (strncmp(line, "processor", 9) == 0) {
                    num_processors_++;
                }
                if (strncmp(line, "physical", 8) == 0) {
                    num_physical_processors_ = ParseLine(line);
                }
            }
            fclose(file);
        } 
--total_ram_ = GetPhysicalMemory();
--std::pair<int64_t, int64_t> in_and_out_octets = Octets();
--in_octets_ = in_and_out_octets.first;                    
--out_octets_ = in_and_out_octets.second;                  
--net_time_ = std::chrono::system_clock::now();            

```