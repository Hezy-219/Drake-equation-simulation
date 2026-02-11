from datetime import datetime
import time
from zoneinfo import ZoneInfo, ZoneInfoNotFoundError
import json
from json.decoder import JSONDecodeError
class DrakeEquation:
  def __init__(self, NOG, R, fp, ne, fl, fi, fc, L, TSIG):
    self.R = R
    self.fp = fp
    self.ne = ne
    self.fl =fl
    self.fi = fi
    self.fc = fc
    self.L = L
    self.TSIG = TSIG
    self.NOG = NOG
    self.First = None
    self.time_now_log = datetime.now(ZoneInfo("America/Toronto"))

  def Calculation(self):
    print("booting up...")
    dt = time.perf_counter()
    time.sleep(5)
    self.First = self.R * self.fp * self.ne * self.fl * self.fi * self.fc * self.L
    print(f"There would be {self.First:.0f} civilizations in {self.NOG}")
    self.prob_1 = self.First/self.TSIG
    print(f'The probability of {self.NOG} having civilizations would be {self.prob_1:.6f}')
    self.prob_2 = 1-(1-self.prob_1)**100
    print(f'The probability of a 100 stars in {self.NOG} having civilizations would be {self.prob_2:.2%}')
    et = time.perf_counter()
    end = et-dt
    print(f'Thought for {end:.0f} seconds')

  def load(self, body_name):
    try:
        with open("log.json", "r") as file:
            data = json.load(file)

            if body_name in data:
                history = data[body_name]

                self.R = history.get("Rate_star_form", self.R)
                self.fp = history.get("Star/plan", self.fp)
                self.ne = history.get("hab_plan/star_sys", self.ne)
                self.fl = history.get("frac_hab_planlife_dev", self.fl)
                self.fi = history.get("frac_plan_intel_life_form", self.fi)
                self.fc = history.get("frac_civi_dev_detect_tech", self.fc)
                self.L = history.get("ave_lifespan_comms_civi", self.L)

                print(f"Successfully loaded history for {body_name}")
            else:
                print(f"No entry found for {body_name} in the logs.")

    except (FileNotFoundError, json.JSONDecodeError):
        print("Log not created or is empty/corrupt.")

  def save(self):
      try:
        with open("log.json", "r") as file:
          data = json.load(file)
      except (FileNotFoundError, json.JSONDecodeError):
        data = {}
      save_time = datetime.now(ZoneInfo("America/Toronto"))
      data[self.NOG] = {
          "Rate_star_form": self.R,
          "Star/plan": self.fp,
          "hab_plan/star_sys": self.ne,
          "frac_hab_planlife_dev": self.fl,
          "frac_plan_intel_life_form": self.fi,
          "frac_civi_dev_detect_tech": self.fc,
          "ave_lifespan_comms_civi": self.L,
          "time_of_rec": str(self.time_now_log),
          "save_time" : str(save_time)
          }
      with open("log.json", "w") as file:
        json.dump(data, file, indent=4)
        print(f"data saved for {self.NOG}")
