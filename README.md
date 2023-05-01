# Animation-Tools
//Keyframe Tool
#include <GL/glut.h>
#include <vector>

struct Keyframe {
    float position[3];
    float rotation[3];
    float scale[3];
};

std::vector<Keyframe> timeline;

void display() {
    glClear(GL_COLOR_BUFFER_BIT);

    // TODO: Set object position, rotation, and scale based on the current keyframe

    glutSolidCube(1.0f); // Replace with your object here

    glutSwapBuffers();
}

int main(int argc, char** argv) {
    glutInit(&argc, argv);
    glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGB);
    glutInitWindowSize(400, 400);
    glutCreateWindow("Keyframe Animation");

    // TODO: Set up timeline and keyframes

    glutDisplayFunc(display);
    glutMainLoop();
    return 0;
}
//Graphics Tool
#include <GL/glut.h>

float angle = 0.0f;
float rotationSpeed = 0.1f;

void update() {
    // Update angle based on rotation speed
    angle += rotationSpeed;
}

void display() {
    glClear(GL_COLOR_BUFFER_BIT);

    // Draw object at current angle
    glPushMatrix();
    glRotatef(angle, 0.0f, 0.0f, 1.0f);
    glutSolidCube(1.0f);
    glPopMatrix();

    glutSwapBuffers();
}

void timer(int value) {
    update();
    glutPostRedisplay();
    glutTimerFunc(16, timer, 0); // 60 FPS
}

int main(int argc, char** argv) {
    glutInit(&argc, argv);
    glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGB);
    glutInitWindowSize(400, 400);
    glutCreateWindow("Graphics Animation");

    glutDisplayFunc(display);
    glutTimerFunc(16, timer, 0); // 60 FPS
    glutMainLoop();
    return 0;
}
// Physics Tool
#include <GL/glut.h>
#include <cmath>

float x = 0.0f; // position
float v = 0.0f; // velocity
const float k = 1.0f; // spring constant
const float m = 1.0f; // mass
const float dt = 0.01f; // time step

void update() {
    float a = -k/m * x; // acceleration from Hooke's law
    v += a * dt; // update velocity
    x += v * dt; // update position
}

void display() {
    glClear(GL_COLOR_BUFFER_BIT);

    // Draw object at current position
    glPushMatrix();
    glTranslatef(x, 0.0f, 0.0f);
    glutSolidSphere(0.1f, 20, 20);
    glPopMatrix();

    glutSwapBuffers();
}

void timer(int value) {
    update();
    glutPostRedisplay();
    glutTimerFunc(16, timer, 0); // 60 FPS
}

int main(int argc, char** argv) {
    glutInit(&argc, argv);
    glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGB);
    glutInitWindowSize(400, 400);
    glutCreateWindow("Physics Animation");

    glutDisplayFunc(display);
    glutTimerFunc(16, timer, 0); // 60 FPS
    glutMainLoop();
    return 0;
}
