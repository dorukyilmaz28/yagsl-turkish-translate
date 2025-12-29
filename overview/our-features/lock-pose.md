---
description: YAGSL'in bunun için bir yardımcısı var!
---

# Pose Kilitleme

## Lock Pose Nedir?

Lock Pose, robotun mevcut pozisyonunu korumak ve dış kuvvetlerle itilmesini veya döndürülmesini zorlaştırmak için kullanılan özel bir durumdur. Bu durumda tüm tekerlekler, birbirine zıt yönlerde olacak şekilde X formasyonuna döndürülür. Böylece robot pasif olarak kilitlenmiş gibi davranır.

Lock Pose yalnızca herhangi bir sürüş girdisi verilmediğinde kullanılmalıdır. Aynı anda sürüş komutu uygulanması, sistemde çakışmalara yol açabilir ve tanımsız veya beklenmeyen davranışların ortaya çıkmasına neden olabilir.

## Lock Pose'u Nasıl Kullanırım?

Herhangi bir kontrolcü girdisi iletmek yerine [`SwerveDrive.lockPose()`](https://broncbotz3481.github.io/YAGSL-Lib/docs/swervelib/SwerveDrive.html#lockPose\(\)) fonksiyonunu tekrar tekrar çağırırsınız.

<pre class="language-java"><code class="lang-java">public class RobotContainer
{

  // Replace with CommandPS4Controller or CommandJoystick if needed
  final CommandXboxController driverXbox = new CommandXboxController(0);
  // The robot's subsystems and commands are defined here...
  private final SwerveSubsystem drivebase = new SwerveSubsystem(new File(Filesystem.getDeployDirectory(),
                                                                         "swerve/neo"));

  /**
   * The container for the robot. Contains subsystems, OI devices, and commands.
   */
  public RobotContainer()
  {
    // Configure the trigger bindings
    configureBindings();

    Command driveFieldOrientedDirectAngleSim = drivebase.simDriveCommand(
        () -> MathUtil.applyDeadband(driverXbox.getLeftY(), OperatorConstants.LEFT_Y_DEADBAND),
        () -> MathUtil.applyDeadband(driverXbox.getLeftX(), OperatorConstants.LEFT_X_DEADBAND),
        () -> driverXbox.getRawAxis(2));

    drivebase.setDefaultCommand(driveFieldOrientedDirectAngleSim);
  }

  /**
   * Use this method to define your trigger->command mappings. Triggers can be created via the
   * {@link Trigger#Trigger(java.util.function.BooleanSupplier)} constructor with an arbitrary predicate, or via the
   * named factories in {@link edu.wpi.first.wpilibj2.command.button.CommandGenericHID}'s subclasses for
   * {@link CommandXboxController Xbox}/{@link edu.wpi.first.wpilibj2.command.button.CommandPS4Controller PS4}
   * controllers or {@link edu.wpi.first.wpilibj2.command.button.CommandJoystick Flight joysticks}.
   */
  private void configureBindings()
  {
<strong>    driverXbox.x().whileTrue(Commands.runOnce(drivebase::lock, drivebase).repeatedly());
</strong>  }

  /**
   * Use this to pass the autonomous command to the main {@link Robot} class.
   *
   * @return the command to run in autonomous
   */
  public Command getAutonomousCommand()
  {
    // An example command will be run in autonomous
    return drivebase.getAutonomousCommand("New Auto");
  }

  public void setDriveMode()
  {
    //drivebase.setDefaultCommand();
  }

  public void setMotorBrake(boolean brake)
  {
    drivebase.setMotorBrake(brake);
  }
}

</code></pre>
