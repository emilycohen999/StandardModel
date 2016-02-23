package com.qualcomm.ftcrobotcontroller.opmodes;

/**
 * Created by student on 9/25/15.
 */
import android.drm.DrmStore;

import com.qualcomm.robotcore.eventloop.opmode.OpMode;
import com.qualcomm.robotcore.hardware.DcMotor;
import com.qualcomm.robotcore.hardware.Servo;
import com.qualcomm.robotcore.util.Range;

/**
 * TeleOp Mode
 * <p>
 * Enables control of the robot via the gamepad
 */
public class NewDrive extends OpMode {

    DcMotor motorLeftFront;
    DcMotor motorLeftBack;
    DcMotor motorRightFront;
    DcMotor motorRightBack;
    DcMotor motorPullUp;
    DcMotor motorextensionLeft;
    DcMotor motorextensionRight;
    DcMotor motorNom;
    //DcMotor motorClimber;

    Integer encextleft;
    Integer encextright;

    //Servo triggers;
    Servo box;
    Servo aiming;
    Servo hook1;
    Servo hook2;
    Servo ramp;

    /*
     * Code to run when the op mode is first enabled goes here
     *
     * @see com.qualcomm.robotcore.eventloop.opmode.OpMode#start()
     */
    @Override
    public void init() {
		/*
		 * Use the hardwareMap to get the dc motors and servos by name. Note
		 * that the names of the devices must match the names used when you
		 * configured your robot and created the configuration file.
		 */

        motorLeftFront = hardwareMap.dcMotor.get("left_front");
        motorLeftBack = hardwareMap.dcMotor.get("left_back");
        motorPullUp = hardwareMap.dcMotor.get("motor_up");
        motorRightFront = hardwareMap.dcMotor.get("right_front");
        motorRightBack = hardwareMap.dcMotor.get("right_back");
        motorextensionLeft = hardwareMap.dcMotor.get("extension_left");
        motorextensionRight = hardwareMap.dcMotor.get("extension_right");
        motorNom = hardwareMap.dcMotor.get("nom");

        //motorClimber = hardwareMap.dcMotor.get("motor_climber");
        //climbers = hardwareMap.servo.get("servo_1");


        aiming = hardwareMap.servo.get("servo_2");
        hook2 = hardwareMap.servo.get("servo_3");
        hook1 = hardwareMap.servo.get("servo_4");
        box = hardwareMap.servo.get("servo_5");
        ramp = hardwareMap.servo.get("servo_6");


        motorLeftFront.setDirection(DcMotor.Direction.REVERSE);
        motorLeftBack.setDirection(DcMotor.Direction.REVERSE);
        motorextensionLeft.setDirection(DcMotor.Direction.REVERSE);
        hook1.setPosition(.8);
        hook2.setPosition(.8);


    }

    /*
     * This method will be called repeatedly in a loop
     *
     * @see com.qualcomm.robotcore.eventloop.opmode.OpMode#run()
     */
    //double servoPosition = 0;
    double aimPosition = 0.5;
    double hookPosition = 0;
    double rampPosition = 0;
    @Override
    public void loop() {

        encextleft = motorextensionLeft.getCurrentPosition();
        encextright = motorextensionRight.getCurrentPosition();

        // note that if y equal -1 then joystick is pushed all of the way forward.
        float frontPower = -gamepad1.left_stick_y;
        float spinPower = -gamepad1.right_stick_y;
        float nomPower = -gamepad2.right_stick_y;
        float extensionPower = gamepad2.left_stick_y;
//        float upPowerWinch = gamepad2.right_trigger;
//        float downPowerWinch = -gamepad2.left_trigger;
        frontPower = -frontPower;
        // clip the right/left values so that the values never exceed +/- 1

        frontPower = Range.clip(frontPower, -1, 1);
        spinPower = Range.clip(spinPower, -1, 1);
//        upPowerWinch = Range.clip(upPowerWinch, -1, 1);
//        downPowerWinch = Range.clip(downPowerWinch, -1, 1);
        nomPower = Range.clip(nomPower, -1, 1);
        extensionPower = Range.clip(extensionPower, -1,1);


        // scale the joystick value to make it easier to control
        // the robot more precisely at slower speeds.
        frontPower = (float)scaleInput(frontPower);
        spinPower =  (float)scaleInput(spinPower);
//        upPowerWinch = (float)scaleInput(upPowerWinch);
//        downPowerWinch = (float)scaleInput(downPowerWinch);
        extensionPower = (float)scaleInput(extensionPower);
        nomPower = (float)scaleInput(nomPower);

        // write the values to the motors, aka drive
        if(Math.abs(gamepad1.right_stick_y) >= 0.2) {
            motorRightFront.setPower(-spinPower);
            motorLeftFront.setPower(spinPower);
            motorRightBack.setPower(-spinPower);
            motorLeftBack.setPower(spinPower);
        } else {
            motorRightFront.setPower(frontPower);
            motorLeftFront.setPower(frontPower);
            motorRightBack.setPower(frontPower);
            motorLeftBack.setPower(frontPower);
        }

    //code for the extension
        if (Math.abs(gamepad2.left_stick_y)>=.2){
//            if(extensionPower<0 && (encextleft<(-3100) || encextright<(-3100))){
//            }
//            else if (extensionPower>0 && (encextleft>(-200)||encextright>(-200))){
//            }
           // else{
                motorextensionLeft.setPower(extensionPower);
                motorextensionRight.setPower(extensionPower);
           // }
        }
        else if(!gamepad2.x && !gamepad2.y && !gamepad2.a && !gamepad2.b){
            motorextensionLeft.setPower(0);
            motorextensionRight.setPower(0);
        }

        //power to the nom
        if(Math.abs(gamepad2.right_stick_y)>=.2) {
            motorNom.setPower(nomPower);
        } else {
            motorNom.setPower(0);
        }

        //pull up
        if(gamepad2.dpad_right){
            motorPullUp.setPower(.8);
        }
        else if(gamepad2.dpad_left){
            motorPullUp.setPower(-.8);
        }
        else{
            motorPullUp.setPower(0);
        }


        // update the position of the arm.
        if (gamepad1.a) {
            // if the A button is pushed on gamepad1, increment the position of
            // the arm servo.
            //armPosition += armDelta;
        }

        if (gamepad1.y) {
            // if the Y button is pushed on gamepad1, decrease the position of
            motorRightFront.setPower(0);
            motorRightBack.setPower(0);
            motorLeftBack.setPower(0);
            motorLeftFront.setPower(0);
        }

        //code for the box
        if(gamepad1.left_trigger <= 1 && gamepad1.left_trigger >= 0 && gamepad1.right_trigger <= 1 && gamepad1.right_trigger >= 0) {
            if (gamepad1.left_trigger > 0.25) {
                box.setPosition(0.5 - gamepad1.left_trigger / 2);
            }
            if (gamepad1.right_trigger > 0.25) {
                box.setPosition(0.5 + gamepad1.right_trigger / 2);
            }
            if (gamepad1.right_trigger < 0.25 && gamepad1.left_trigger < 0.25) {
                box.setPosition(0.493);
            }
        } else {
            box.setPosition(0.493);
        }


        //entension singles
        if(gamepad2.x){
            motorextensionLeft.setPower(.5);
            motorextensionRight.setPower(0);
        }
        if(gamepad2.y){
            motorextensionLeft.setPower(-.5);
            motorextensionRight.setPower(0);
        }

        if(gamepad2.a){
            motorextensionRight.setPower(.5);
            motorextensionLeft.setPower(0);
        }
        if(gamepad2.b){
            motorextensionRight.setPower(-.5);
            motorextensionLeft.setPower(0);
        }

        //hooks
        if(Math.abs(gamepad2.right_trigger) > 0.2) {
            hook1.setPosition(0.5 + gamepad2.right_trigger/2);
            hook2.setPosition(0.5 - gamepad2.right_trigger/2);
        } else if(Math.abs(gamepad2.left_trigger) > 0.2) {
            hook1.setPosition(0.5 - gamepad2.left_trigger/2);
            hook2.setPosition(0.5 + gamepad2.left_trigger/2);
        } else {
        }

//aim the pull up
        if(gamepad2.dpad_down) {
            if(aimPosition + 0.01 <= 1) {
                aimPosition += 0.01;
            }
            aiming.setPosition(aimPosition);
        }
        if(gamepad2.dpad_up) {
            if(aimPosition - 0.01 >= 0) {
                aimPosition -= 0.01;
            }
            aiming.setPosition(aimPosition);
        }


//ramp
        if(gamepad2.left_bumper) {
            if(rampPosition + 0.01 <= 1) {
                rampPosition += 0.01;
            }
            ramp.setPosition(rampPosition);
        }
        if(gamepad2.right_bumper) {
            if(rampPosition - 0.01 >= 0) {
                rampPosition -= 0.01;
            }
            ramp.setPosition(rampPosition);
        }

        if (gamepad1.b) {
            //clawPosition -= clawDelta;
        }

        // update the position of the claw
        if (gamepad1.x) {
            //clawPosition += clawDelta;
        }

        if (gamepad1.b) {
            //clawPosition -= clawDelta;
        }

		/*
		 * Send telemetry data back to driver station. Note that if we are using
		 * a legacy NXT-compatible motor controller, then the getPower() method
		 * will return a null value. The legacy NXT-compatible motor controllers
		 * are currently write only.
		 */
        telemetry.addData("extension right", encextleft);
        telemetry.addData("extension left", encextright);
    }

    /*
     * Code to run when the op mode is first disabled goes here
     *
     * @see com.qualcomm.robotcore.eventloop.opmode.OpMode#stop()
     */
    @Override
    public void stop() {

    }

    /*
     * This method scales the joystick input so for low joystick values, the
     * scaled value is less than linear.  This is to make it easier to drive
     * the robot more precisely at slower speeds.
     */
    double scaleInput(double dVal)  {
        double[] scaleArray = { 0.0, 0.05, 0.09, 0.10, 0.12, 0.15, 0.18, 0.24,
                0.30, 0.36, 0.43, 0.50, 0.60, 0.72, 0.85, 1.00, 1.00 };

        // get the corresponding index for the scaleInput array.
        int index = (int) (dVal * 16.0);

        // index should be positive.
        if (index < 0) {
            index = -index;
        }

        // index cannot exceed size of array minus 1.
        if (index > 16) {
            index = 16;
        }

        // get value from the array.
        double dScale = 0.0;
        if (dVal < 0) {
            dScale = -scaleArray[index];
        } else {
            dScale = scaleArray[index];
        }
        // return scaled value.
        return dScale;
    }

}
