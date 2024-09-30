# Postest1_PBO
# Muhammad Danil Pratama
# 2309116091
# Sistem Informasi B

/*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 * Click nbfs://nbhost/SystemFileSystem/Templates/Classes/Class.java to edit this template
 */
package manajemen;

import models.Container;
import models.ContainerManager;
import java.util.Scanner;

public class MainApp {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        ContainerManager manager = new ContainerManager();
        boolean exit = false;

        // Menambahkan 5 container secara otomatis
        manager.addContainer(new Container("C001", "Refrigerated", 1000.5));
        manager.addContainer(new Container("C002", "Dry", 2000.75));
        manager.addContainer(new Container("C003", "Flat Rack", 1500.3));
        manager.addContainer(new Container("C004", "Tank", 1800.1));
        manager.addContainer(new Container("C005", "Open Top", 2200.8));

        while (!exit) {
            System.out.println("\n==== Manajemen Sistem Peti Kemas ====");
            System.out.println("1. Tambah Container");
            System.out.println("2. Tampilkan Semua Container");
            System.out.println("3. Update Container");
            System.out.println("4. Hapus Container");
            System.out.println("5. Keluar");
            System.out.print("Pilih opsi: ");
            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline

            switch (choice) {
                case 1:
                    System.out.print("Masukkan ID Container: ");
                    String id = scanner.nextLine();
                    System.out.print("Masukkan Tipe Container: ");
                    String type = scanner.nextLine();
                    System.out.print("Masukkan Berat Container (kg): ");
                    double weight = scanner.nextDouble();
                    Container container = new Container(id, type, weight);
                    manager.addContainer(container);
                    break;

                case 2:
                    manager.displayAllContainers();
                    break;

                case 3:
                    System.out.print("Masukkan ID Container yang akan di-update: ");
                    String updateId = scanner.nextLine();
                    System.out.print("Masukkan Tipe Baru: ");
                    String newType = scanner.nextLine();
                    System.out.print("Masukkan Berat Baru (kg): ");
                    double newWeight = scanner.nextDouble();
                    manager.updateContainer(updateId, newType, newWeight);
                    break;

                case 4:
                    System.out.print("Masukkan ID Container yang akan dihapus: ");
                    String deleteId = scanner.nextLine();
                    manager.deleteContainer(deleteId);
                    break;

                case 5:
                    exit = true;
                    System.out.println("Keluar dari sistem.");
                    break;

                default:
                    System.out.println("Opsi tidak valid.");
                    break;
            }

/*
 * Click nbfs://nbhost/SystemFileSystem/Templates/Licenses/license-default.txt to change this license
 * Click nbfs://nbhost/SystemFileSystem/Templates/Classes/Class.java to edit this template
 */
package models;

import java.util.ArrayList;

public class ContainerManager {
    private ArrayList<Container> containers = new ArrayList<>();
    public static int totalContainers = 0; // Static keyword

    // Method to add a container
    public void addContainer(Container container) {
        containers.add(container);
        totalContainers++;
        System.out.println("Container added successfully!");
    }

    // Method to display all containers
    public void displayAllContainers() {
        if (containers.isEmpty()) {
            System.out.println("No containers available.");
        } else {
            for (Container container : containers) {
                container.displayInfo();
                System.out.println("------------");
            }
        }
    }

    // Method to update a container
    public void updateContainer(String id, String newType, double newWeight) {
        boolean found = false;
        for (Container container : containers) {
            if (container.getId().equals(id)) {
                container.setType(newType);
                container.setWeight(newWeight);
                System.out.println("Container updated successfully!");
                found = true;
                break;
            }
        }
        if (!found) {
            System.out.println("Container with ID " + id + " not found.");
        }
    }

    // Method to delete a container
    public void deleteContainer(String id) {
        boolean found = false;
        for (Container container : containers) {
            if (container.getId().equals(id)) {
                containers.remove(container);
                totalContainers--;
                System.out.println("Container deleted successfully!");
                found = true;
                break;
            }
        }
        if (!found) {
            System.out.println("Container with ID " + id + " not found.");
        }
    }
}

            System.out.println("Total container saat ini: " + ContainerManager.totalContainers);
        }

        scanner.close();
    }
}
