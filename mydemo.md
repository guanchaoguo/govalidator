package main

import (
	"github.com/asaskevich/govalidator"

)

func init() {
	govalidator.SetFieldsRequiredByDefault(true)
}

type Ticket struct {
	Id        int64     `json:"id" valid:"-"`
	FirstName string    `json:"firstname" valid:"required~请填写名称"`
	AuthorIP string     `json:"authorIP"  valid:"required~请填写IP,ipv4~请填写有效IP"`
}




func main() {
	ticket := &Ticket{
		Id:  100,
		FirstName: "",
		AuthorIP: "192.168.31.266",
	}

	result, err := govalidator.ValidateStruct(ticket)
	if err != nil {
		println("error: " + err.Error())
	}
	println(result)
}
