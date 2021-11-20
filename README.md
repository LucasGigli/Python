class Employee:
  Employees = {}
  Std_rate = 0.2
  Higher_rate = 0.4

  def __init__(self,StaffID,LastName,FirstName,RegHours,HourlyRate,OTMultiple,TaxCredit,StandardBand):
    self.Employees = {}
    self.StaffID = StaffID
    self.LastName = LastName
    self.FirstName = FirstName
    self.RegHours = RegHours
    self.HourlyRate = HourlyRate
    self.OTMultiple = OTMultiple
    self.TaxCredit = TaxCredit
    self.StandardBand = StandardBand


  def setup(Employeesfile):
      with open(Employeesfile) as f:
        for line in f:
          StaffID,LastName,FirstName,RegHours,HourlyRate,OTMultiple,TaxCredit,StandardBand = line.split()
          Employee.Employees[StaffID] = Employee(StaffID,LastName,FirstName,float(RegHours),float(HourlyRate),float(OTMultiple),float(TaxCredit),float(StandardBand)) 

  def ComputePayment(self, Hours, HoursWorked, Date):
    with open (Hours) as f1:
      for line in f1:
        HoursWorked = float (HoursWorked) ; Date = str(Date)
        CP = {}
        HoursWOrked = 0 
        if self.RegHours > HoursWorked:
          Rh = HoursWorked 
        if HoursWorked > self.RegHours:
          Oh = HoursWorked - self.RegHours
        else:
          Oh = HoursWorked 
        Or = self.OTMultiple * self.HourlyRate
        Rp = self.RegHours*self.HourlyRate
        if HoursWorked > self.RegHours:
          Op = (float(HoursWorked) - self.RegHours) * (self.OTMultiple * self.HourlyRate)
        else:
          Op = 0
        if float(HoursWorked)> self.RegHours:
          Gp = ((float(HoursWorked) - self.RegHours ) * (self.OTMultiple * self.HourlyRate)) + (self.RegHours * self.HourlyRate)
        else:
          Gp= float(HoursWorked)*self.HourlyRate
        if HoursWorked > self.RegHours:
          Hrp = ((float(HoursWorked) - self.RegHours ) * (self.OTMultiple * self.HourlyRate))
        else:
          Hrp = 0 
        Stax = self.StandardBand * Employee.Std_rate
        if Gp > self.StandardBand:
          Htax = (Gp - self.StandardBand) * Employee.Higher_rate
        else:
          Htax = 0 
        if Gp > self.StandardBand:
          T = Stax + Htax
        else:
          T = Stax
        Nd = T - self.TaxCredit
        NetPay = Gp - Nd 
        CP = {f'Name: {self.FirstName} {self.LastName}, Date: {Date}, Regular Hours Worked: {Rh}, Overtime Hours Worked: {Oh}, Regular Rate: {self.HourlyRate}, Overtime Rate: {Or}, Regular Pay: {Rp}, Overtime Pay: {Op}, Gross Pay: {Gp}, Standard Rate Pay: {self.StandardBand}, Higher Rate Pay: {Hrp}, Standard Tax: {Stax}, Higher Tax: {Htax}, Total Tax: {T}, Net Deductions: {Nd}, Net Pay {NetPay}' } 
        return print(CP)

Employee.setup('Employees.txt')
jg = Employee('12345','Green','Joe',37,16,1.5,70,700)
jg.ComputePayment('Hours.txt',15,'31/10/21')

                                          
