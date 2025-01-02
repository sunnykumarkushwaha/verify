# verify

<br>
<h3>hey its me </h3>
<h3>hey its me </h3



import React, { useState, useRef, useEffect } from "react";
import { Button, Offcanvas } from "react-bootstrap";

const CustomScrollDatePicker = () => {
  const [showOffcanvas, setShowOffcanvas] = useState(false);
  const [day, setDay] = useState("01");
  const [month, setMonth] = useState("01");
  const [year, setYear] = useState(new Date().getFullYear().toString());

  const days = Array.from({ length: 31 }, (_, i) =>
    String(i + 1).padStart(2, "0")
  );
  const months = Array.from({ length: 12 }, (_, i) =>
    String(i + 1).padStart(2, "0")
  );
  const years = Array.from(
    { length: 60 },
    (_, i) => String(new Date().getFullYear() - i)
  );

  const handleShowOffcanvas = () => setShowOffcanvas(true);
  const handleCloseOffcanvas = () => setShowOffcanvas(false);

  // Scroll event handler to find the closest value
  const handleScroll = (e, options, setValue) => {
    const scrollTop = e.target.scrollTop;
    const index = Math.round(scrollTop / 40); // Assuming each option is 40px tall
    const selectedValue = options[index];
    if (selectedValue) {
      setValue(selectedValue);
      console.log(`Selected: ${selectedValue}`);
    }
  };

  return (
    <div>
      {/* Button to Open Date Picker */}
      <Button variant="primary" onClick={handleShowOffcanvas}>
        Open Date Picker
      </Button>

      {/* Offcanvas Date Picker */}
      <Offcanvas
        show={showOffcanvas}
        onHide={handleCloseOffcanvas}
        placement="bottom"
      >
        <Offcanvas.Header closeButton>
          <Offcanvas.Title>Select a Date</Offcanvas.Title>
        </Offcanvas.Header>
        <Offcanvas.Body>
          <div
            style={{
              display: "flex",
              justifyContent: "space-around",
              alignItems: "center",
              height: "200px",
            }}
          >
            {/* Day Picker */}
            <div style={{ width: "100px", overflow: "hidden" }}>
              <div
                onScroll={(e) => handleScroll(e, days, setDay)}
                style={{
                  height: "120px",
                  overflowY: "scroll",
                  textAlign: "center",
                }}
              >
                {days.map((d, i) => (
                  <div
                    key={i}
                    style={{
                      height: "40px",
                      lineHeight: "40px",
                      fontSize: d === day ? "18px" : "16px",
                      fontWeight: d === day ? "bold" : "normal",
                    }}
                  >
                    {d}
                  </div>
                ))}
              </div>
            </div>

            {/* Month Picker */}
            <div style={{ width: "100px", overflow: "hidden" }}>
              <div
                onScroll={(e) => handleScroll(e, months, setMonth)}
                style={{
                  height: "120px",
                  overflowY: "scroll",
                  textAlign: "center",
                }}
              >
                {months.map((m, i) => (
                  <div
                    key={i}
                    style={{
                      height: "40px",
                      lineHeight: "40px",
                      fontSize: m === month ? "18px" : "16px",
                      fontWeight: m === month ? "bold" : "normal",
                    }}
                  >
                    {m}
                  </div>
                ))}
              </div>
            </div>

            {/* Year Picker */}
            <div style={{ width: "100px", overflow: "hidden" }}>
              <div
                onScroll={(e) => handleScroll(e, years, setYear)}
                style={{
                  height: "120px",
                  overflowY: "scroll",
                  textAlign: "center",
                }}
              >
                {years.map((y, i) => (
                  <div
                    key={i}
                    style={{
                      height: "40px",
                      lineHeight: "40px",
                      fontSize: y === year ? "18px" : "16px",
                      fontWeight: y === year ? "bold" : "normal",
                    }}
                  >
                    {y}
                  </div>
                ))}
              </div>
            </div>
          </div>

          {/* Confirm Date Button */}
          <Button
            variant="success"
            onClick={handleCloseOffcanvas}
            style={{ marginTop: "20px" }}
          >
            Confirm Date
          </Button>
        </Offcanvas.Body>
      </Offcanvas>

      {/* Display Selected Date */}
      <div style={{ marginTop: "20px" }}>
        <strong>Selected Date:</strong> {`${day}/${month}/${year}`}
      </div>
    </div>
  );
};

export default CustomScrollDatePicker;

